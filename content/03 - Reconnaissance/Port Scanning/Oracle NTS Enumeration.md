## Footprinting Service
```bash
sudo nmap -p1521 -sV 10.129.204.235 --open
```

---
## Brute-Forcing SID
```bash
sudo nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute
```
Check [[System Identifier (SID)]] to understand what SID is

```bash
# Example Output can look like this
PORT STATE SERVICE VERSION 
1521/tcp open oracle-tns Oracle TNS listener 11.2.0.2.0 (unauthorized) 
| oracle-sid-brute: 
|_ XE
```
- We discover that the SID is XE

---
