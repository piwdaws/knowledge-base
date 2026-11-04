# ❓Question

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

# 📋 Walkthrough 

We need to find a port which speak SSL/TLS. Connect to it and submit the current password to proceed.

For this we can use nmap to scan the port in range 31000 to 32000

```bash
bandit16@bandit:~$ nmap localhost -sC -sV -p 31000-32000
Starting Nmap 7.98 ( https://nmap.org ) at 2026-07-10 08:02 +0000
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00054s latency).
Other addresses for localhost (not scanned): ::1
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
| ssl-cert: Subject: commonName=SnakeOil
| Not valid before: 2024-06-10T03:59:50
|_Not valid after:  2034-06-08T03:59:50
|_ssl-date: TLS randomness does not represent time
31691/tcp open  echo
31790/tcp open  ssl/unknown
| fingerprint-strings: 
|   FourOhFourRequest, GenericLines, GetRequest, HTTPOptions, Help, LPDString, RTSPRequest, SIPOptions: 
|_    Wrong! Please enter the correct current password.
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=SnakeOil
| Not valid before: 2024-06-10T03:59:50
|_Not valid after:  2034-06-08T03:59:50
31960/tcp open  echo
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port31790-TCP:V=7.98%T=SSL%I=7%D=7/10%Time=6A50A72E%P=x86_64-pc-linux-g
SF:nu%r(GenericLines,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x20cu
SF:rrent\x20password\.\n")%r(GetRequest,32,"Wrong!\x20Please\x20enter\x20t
SF:he\x20correct\x20current\x20password\.\n")%r(HTTPOptions,32,"Wrong!\x20
SF:Please\x20enter\x20the\x20correct\x20current\x20password\.\n")%r(RTSPRe
SF:quest,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x20pas
SF:sword\.\n")%r(Help,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x20c
SF:urrent\x20password\.\n")%r(FourOhFourRequest,32,"Wrong!\x20Please\x20en
SF:ter\x20the\x20correct\x20current\x20password\.\n")%r(LPDString,32,"Wron
SF:g!\x20Please\x20enter\x20the\x20correct\x20current\x20password\.\n")%r(
SF:SIPOptions,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x
SF:20password\.\n");

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 124.83 seconds
```

You can use normal search nmap no need to add -sC -sV. I did that out of habit

We see that port 31518 and 31790 got TLS. Just try both. if it return the same password we know its not the right one.

```bash
bandit16@bandit:~$ openssl s_client -connect localhost:31790
Connecting to 127.0.0.1
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
------
read R BLOCK
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
KEYUPDATE

Wrong! Please enter the correct current password.
closed
```

We encounter a KEYUPDATE message. This happen because our password start with k. Reading the Manual shown that certain letter that appear in the start of the line is recognize as command. To prevent this we need to use -quiet option 

```bash
bandit16@bandit:~$ openssl s_client -quiet -connect localhost:31790
Connecting to 127.0.0.1
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
Correct!

[SSH Key redacted]
```

We receive sshkey instead. Copy it and paste in a file