## Footprinting Service
```bash
sudo nmap -sU --script ipmi-version -p 623 ilo.inlanfreight.local
```
```bash
# Example Output
PORT STATE SERVICE 
623/udp open asf-rmcp 
| ipmi-version: 
| Version: 
| IPMI-2.0 
| UserAuth: 
| PassAuth: auth_user, non_null_user 
|_ Level: 2.0
```
- We discover it use IPMI-2.0
- If we google it, this version have unfixable protocol design flaw
- The server require a valid username (auth_user) and we cant leave it blank
- But since its 2.0, as long we can guess the username we can get the password hash
- Because of the design flaw that the server reply us with password hash
- without checking if we even know the pass

---
## Password Hash Dumping

- Refer to [[IPMI Metasploit]] 