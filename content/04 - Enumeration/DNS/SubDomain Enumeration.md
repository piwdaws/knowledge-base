- Understanding what subdomain is [[Subdomain in DNS]]

## Bruteforcing subdomain with dnsenum
```bash
# --enum shortcut switch that enables a bundle of standard enumeration tasks
# -r Enable recursion. If dnsenum found a subdomain,it will attemp to bruteforce that sub-level too
dnsenum --enum inlanefreight.com -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -r
```
```bash
# Example output
www.inlanefreight.com. 300 IN A 134.209.24.248 
support.inlanefreight.com. 300 IN A 134.209.24.248 
[...]
```
- Here we discover a subdomain of support.