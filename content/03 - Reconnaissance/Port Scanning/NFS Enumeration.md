## Footprinting The Service
```bash
sudo nmap 10.129.14.128 -p 111,2049 -sV -sC
```

---
## NSE Script for scan
```bash
sudo nmap --script nfs* 10.129.14.128 -sV -p 111,2049
```

