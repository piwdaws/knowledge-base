## Brute-Forcing VHost with gobuster
```bash
# vhost we perform vhost fuzzing
# --append-domain we tell gobuster to take the wordlist and combine with the base target domain
gobuster vhost -u http://inlanefreight.htb:81 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain
```
```bash
# Example Output
Found: forum.inlanefreight.htb:81 Status: 200 [Size: 100] 
[...]
 Progress: 114441 / 114442 (100.00%)
```
- We discover another service named forum on the same address