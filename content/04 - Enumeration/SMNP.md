## Footprinting with SNMPwalk
```bash
# -v2c we specify the version
# -c public we specify the Community String (password)
# Here we use public as Community String
snmpwalk -v2c -c public 10.129.14.128
```
```bash
# Example Output
iso.3.6.1.2.1.25.6.3.1.2.1232 = STRING: "printer-driver-sag-gdi_0.1-7_all" iso.3.6.1.2.1.25.6.3.1.2.1233 = STRING: "printer-driver-splix_2.0.0+svn315-7fakesync1build1_amd64" 
iso.3.6.1.2.1.25.6.3.1.2.1234 = STRING: "procps_2:3.3.16-1ubuntu2.3_amd64" iso.3.6.1.2.1.25.6.3.1.2.1235 = STRING: "proftpd-basic_1.3.6c-2_amd64" iso.3.6.1.2.1.25.6.3.1.2.1236 = STRING: "proftpd-doc_1.3.6c-2_all" iso.3.6.1.2.1.25.6.3.1.2.1237 = STRING: "psmisc_23.3-1_amd64" iso.3.6.1.2.1.25.6.3.1.2.1238 = STRING: "publicsuffix_20200303.0012-1_all" iso.3.6.1.2.1.25.6.3.1.2.1239 = STRING: "pulseaudio_1:13.99.1-1ubuntu3.12_amd64" iso.3.6.1.2.1.25.6.3.1.2.1240 = STRING: "pulseaudio-module-bluetooth_1:13.99.1-1ubuntu3.12_amd64" 
iso.3.6.1.2.1.25.6.3.1.2.1241 = STRING: "pulseaudio-utils_1:13.99.1-1ubuntu3.12_amd64" 
iso.3.6.1.2.1.25.6.3.1.2.1242 = STRING: "python-apt-common_2.0.0ubuntu0.20.04.6_all" 
iso.3.6.1.2.1.25.6.3.1.2.1243 = STRING: "python3_3.8.2-0ubuntu2_amd64" iso.3.6.1.2.1.25.6.3.1.2.1244 = STRING: "python3-acme_1.1.0-1_all" iso.3.6.1.2.1.25.6.3.1.2.1245 = STRING: "python3-apport_2.20.11-0ubuntu27.21_all" 
iso.3.6.1.2.1.25.6.3.1.2.1246 = STRING: "python3-apt_2.0.0ubuntu0.20.04.6_amd64"
```
- From the output we discover that they got python3 installed. Theres printer also
- But the most important one theres proFTPd 1.3.6. That things got exploit

---
## Bruteforce with OneSixtyOne
- Purpose: Discover / brute-force SNMP community strings
```bash
# -c We specify the wordlist for Community Strings
onesixtyone -c /opt/useful/seclists/Discovery/SNMP/snmp.txt 10.129.14.128
```
```Bash
# Example Output
Scanning 1 hosts, 3220 communities 10.129.14.128 [public] Linux htb 5.11.0-37-generic #41~20.04.2-Ubuntu SMP Fri Sep 24 09:06:38 UTC 2021 x86_64
```
- We discover the Community String is public and other stuff

---
## Brutefore with braa
- Once you get the Community String 
- Purpose: Query / brute-force OIDs once you know the community string
```bash
# The Community String is public
# :.1.3.6.* This is data range pattern of OID
# .1.3.6. Is a standard starting point for almost interesting data
# * the asterisk act as wild card
braa public@10.129.14.128:.1.3.6.*
```
```bash
# Example Output
10.129.14.128:20ms:.1.3.6.1.2.1.1.1.0:Linux htb 5.11.0-34-generic 10.129.14.128:20ms:.1.3.6.1.2.1.1.2.0:.1.3.6.1.4.1.8072.3.2.10 10.129.14.128:20ms:.1.3.6.1.2.1.1.3.0:548 10.129.14.128:20ms:.1.3.6.1.2.1.1.4.0:mrb3n@inlanefreight.htb 10.129.14.128:20ms:.1.3.6.1.2.1.1.5.0:htb 10.129.14.128:20ms:.1.3.6.1.2.1.1.6.0:US 10.129.14.128:20ms:.1.3.6.1.2.1.1.7.0:78 ...SNIP...
```
- We found the kernel version and OS
- We also found the administrator email account (mrb3n@inlanefreight.htb)
- mrb3n might be can be use for username of FTP or other service
