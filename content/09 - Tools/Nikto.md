- Open-source web server scanner that performs rapid, automated vulnerability assessments against web servers.
- Basically it look for security flaw and configuration mistake

--- 
## Installation
```bash
sudo apt update && sudo apt install -y perl
git clone https://github.com/sullo/nikto
cd nikto/program
chmod +x ./nikto.pl
```

---
## Usage
```bash
# -Tuning b is an option for Software Status / Misconfigured Files
# if you didnt specify the Tuning it will use all the available option
# And it can be very noisy
nikto -h target.com -Tuning b
```
```bash
# Example Output
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target Host: target.com
+ Target Port: 443
---------------------------------------------------------------------------
+ SSL Info:        Subject: /CN=target.com
                   Issuer: Let's Encrypt
+ Start Time:      2026-09-18 00:30:00
---------------------------------------------------------------------------
+ Server: Apache/2.4.41 (Ubuntu)
+ /: X-Powered-By: PHP/8.1.2
+ /: Uncommon header 'x-redirect-by' found, with contents: WordPress.
+ /license.txt: License file found may identify site software.
+ /: A Wordpress installation was found.
+ /wp-login.php: Wordpress login found.
+ 1316 requests: 0 error(s) and 5 item(s) reported on remote host
---------------------------------------------------------------------------
+ End Time:        2026-09-18 00:31:10
```
- From the output we know the existence of license.txt
- We discover it software & framework(WP, Apache and PHP)

---
## List of Tuning

0 - File Upload
1 - Interesting File / Seen in Logs
2 - Misconfiguration / Default File
3 - Information Disclosure
4 - Injection (XSS/Script/HTML)
5 - Remote File Retrieval - Web Root
6 - Denial of Service
7 - Remote File Retrieval - Server
8 - Command Execution / Remote Shell
9 - SQL Injection
a - Authentication Bypass
b - Software Identification
c - Remote Source Inclusion
d - Web Service
e - Administrative Console
x - Reverse Tuning (disable specified tuning)