## What is this
- Python-based web reconnaissance tool that combines multiple reconnaissance functions into one tool.

---
## Capabilities 
- HTTP header analysis 
- SSL/TLS certificate information 
- WHOIS lookup 
- Web crawling 
- DNS enumeration 
- Subdomain enumeration 
- Directory enumeration 
- Wayback Machine URL discovery 
- Fast port scanning
---
## Installation
```bash
git clone https://github.com/thewhiteh4t/FinalRecon.git
cd FinalRecon
pip3 install -r requirements.txt
chmod +x ./finalrecon.py
./finalrecon.py --help
# Check the manual for al kind of options
```

---
## Example Usage
```bash
# --headers to retrieve the http header
# --whois perform whois lookup
./finalrecon.py --headers --whois --url http://target.com
```
```bash
# Or we can just go for full recon with --full
./finalrecon.py --full --url http://target.com
```