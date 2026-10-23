- Open-source command-line tool used by penetration testers and security researchers to **identify and fingerprint Web Application Firewalls (WAFs)** protecting a website
- Knowing what WAF is present, we can decide proper technique to bypass the WAF
- Also prevent use being detected.

---
## Installation
```bash
pip3 install git+https://github.com/EnableSecurity/wafw00f
```

---
## Usage
```bash
wafw00f inlanefreight.com
```
```bash
# Example Output
[*] Checking https://inlanefreight.com 
[+] The site https://inlanefreight.com is behind Wordfence (Defiant) WAF. 
[~] Number of requests: 2
```
- We discover that the webpage got Wordfence developed by Defiant protecting it