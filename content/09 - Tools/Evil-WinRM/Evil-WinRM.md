- Gives an actual interactive shell over WinRM, once we already have working creds (from NetExec or elsewhere)

```bash
evil-winrm -i <target-IP> -u <username> -p <password>
```
- Drops us into a PowerShell session on the target