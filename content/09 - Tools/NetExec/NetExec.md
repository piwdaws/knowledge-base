- NetExec (nxc) is for online login attacks + enumeration, mainly against Windows/AD services
- Supports: nfs, ftp, ssh, winrm, smb, wmi, rdp, mssql, ldap, vnc

```bash
netexec <protocol> <target-IP> -u user.list -p password.list
```
- `(Pwn3d!)` in output = valid creds that can also run commands, not just login
- Each protocol has its own extra options, check with `netexec <protocol> -h`

```bash
netexec smb 10.129.42.197 -u user -p password --shares   # list shares + permissions after login
```
- Good for spraying too, see [[05 - Spraying, Stuffing & Default Creds]]

---
- Also used for: dumping SAM/LSA remotely (`--sam`, `--lsa`), AD dictionary attacks, dumping NTDS.dit (`-M ntdsutil`) — see [[02 - Attacking SAM]] and [[06 - Attacking Active Directory and NTDS]]