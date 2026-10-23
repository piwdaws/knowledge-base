Useful when network file transfer unavailable

---
## Windows --> Linux

```powershell
# Encode in Windows machine
[Convert]::ToBase64String((Get-Content -Path "FILE" -Encoding Byte))
```
```bash
# Decode in linux Machine
echo '<base64>' | base64 -d > file
```

## Linux --> Windows

```bash
# Encode in Linux machine
base64 -w 0 <file name>
```
```powershell
# Decode in Window Machine
[IO.File]::WriteAllBytes( "C:\path\file", [Convert]::FromBase64String("<base64>") )
```

## Verify Integrity

### Windows
```powershell
Get-FileHash <file name> -Algorithm MD5
```

### Linux
```bash
md5sum <file name>
```

## Limitation
- Windows `cmd.exe` has an 8,191-character maximum command-line string length, so this becomes impractical for large files.

---

