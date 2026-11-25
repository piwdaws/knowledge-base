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
```
See [[LaZagne]] for the full tool note (it also works the same way on Linux, see [[Credentials Hunting]] (Linux version) for that side).

## Other places worth checking
- `unattend.xml` (used during Windows install, sometimes has admin password)
- scripts/configs on shared IT drives (SYSVOL share on a DC especially)
- AD user/computer **description field** (admins sometimes dump the password there as a note, don't ask why)
- files literally named `password.txt`, `passwords.xlsx`

---

See also: [[Credential Hunting in Network Traffic]] · [[Credential Hunting in Network Share]] for hunting beyond the local machine