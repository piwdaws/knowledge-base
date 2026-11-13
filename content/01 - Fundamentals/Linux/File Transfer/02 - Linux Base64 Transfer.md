- Useful when normal network file transfer unavailable but you have terminal access

---

## Linux --> Linux
- Encode the file 
```bash
base64 -w 0 file
```
- From victim machine Linux, decode the file
```bash
echo -n '<base64>' | base64 -d > file
```
- Verify its with md5sum
```bash
md5sum file
```
