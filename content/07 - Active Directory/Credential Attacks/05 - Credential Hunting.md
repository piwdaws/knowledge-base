- After landing on a Windows box, search it manually for creds left in files, browsers, configs, before jumping to heavier attacks

## What to search for
- common keywords: `password`, `passwd`, `pwd`, `creds`, `login`, `config`

```cmd
findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml *.ps1 *.yml
```
- `/S` = search subfolders, `/I` = case-insensitive, `/M` = only print filenames

## LaZagne (pulls saved creds from installed apps)
```cmd
LaZagne.exe all

# Example Output
------------------- Winscp passwords -----------------  
[+] Password found !!!  
URL: 10.129.202.51  
Login: admin  
Password: SteveisReallyCool123
```

- checks browsers, chat apps, mail clients, sysadmin tools (WinSCP, OpenVPN), wifi, and Windows creds all in one go
- browsers are the most common hit, since Chrome/Edge/Firefox save logins by default

## Other places worth checking
- `unattend.xml` (used during Windows install, sometimes has admin password)
- scripts/configs on shared IT drives (SYSVOL share on a DC especially)
- AD user/computer **description field** (admins sometimes dump the password there as a note, don't ask why)
- files literally named `password.txt`, `passwords.xlsx`