## DNS Enumeration For NS Query
Some misconfigured DNS server will tell us if the server got another network they trust
Since DNS server is passive we need to ask them what other network they trust
```bash
# We use @ so that we ask directly to the server instead to our local Internet Provider
dig ns inlanefreight.htb @10.129.14.128
```
```bash
; <<>> DiG 9.16.1-Ubuntu <<>> ns inlanefreight.htb @10.129.14.128 
;; global options: +cmd 
;; Got answer: 
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 45010 
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 2 
;; OPT PSEUDOSECTION: ; EDNS: version: 0, flags:; udp: 4096 ; COOKIE: ce4d8681b32abaea0100000061475f73842c401c391690c7 (good) 
;; QUESTION SECTION: ;inlanefreight.htb. IN NS 
;; ANSWER SECTION: inlanefreight.htb. 604800 IN NS ns.inlanefreight.htb. 
;; ADDITIONAL SECTION: ns.inlanefreight.htb. 604800 IN A 10.129.34.136 
;; Query time: 0 msec 
;; SERVER: 10.129.14.128#53(10.129.14.128) 
;; WHEN: So Sep 19 18:04:03 CEST 2021 
;; MSG SIZE rcvd: 107
```
Here an example output. We discover another IP address 10.129.34.136

---
## Version Query
```bash
dig CH TXT version.bind 10.129.120.85
```

---
# ANY Query
ANY option can be use to view all available record. This will show all available entries
```bash
dig any inlanefreight.htb @10.129.14.128
```
```bash
# Example Output
inlanefreight.htb. 604800 IN TXT "v=spf1 include:mailgun.org 
include:_spf.google.com include:spf.protection.outlook.com include:_spf.atlassian.net ip4:10.129.124.8 ip4:10.129.127.2 ip4:10.129.42.106 ~all" 

inlanefreight.htb. 604800 IN TXT "atlassian-domain-verification=t1rKCy68JFszSdCKVpw64A1QksWdXuYFUeSXKU" 

inlanefreight.htb. 604800 IN TXT "MS=ms97310371" 

inlanefreight.htb. 604800 IN SOA inlanefreight.htb. 

root.inlanefreight.htb. 2 604800 86400 2419200 604800 

inlanefreight.htb. 604800 IN NS ns.inlanefreight.htb.
```
The output show us 3 hidden IP Address (SPF Record)
We know know their 3rd party services like mailgun, Google and outlook
And we discover SOA (Start of Authority) with serial number 2

---
## AXFR Zone Transfer
[[Zone Transfer AXFR]] Refer this notes to understand more about Zone Transfer

```bash
# @<DNS server> we say dont use normal DNS reolver but directly send our request to this server
# inlanefreight.htb is DNS Zone that we request
# So we ask the DNS server for complete DNS Record belong to inlanefreight.htb 
dig axfr @10.129.14.128 inlanefreight.htb
```

```bash
# Example Output 
inlanefreight.htb. 604800 IN SOA 
inlanefreight.htb. root.inlanefreight.htb. 2 604800 86400 2419200 604800 inlanefreight.htb. 604800 IN TXT "MS=ms97310371" 
inlanefreight.htb. 604800 IN TXT "atlassian-domain-verification=t1rKCy68JFszSdCKVpw64A1QksWdXuYFUeSXKU" 
inlanefreight.htb. 604800 IN TXT "v=spf1 include:mailgun.org include:_spf.google.com include:spf.protection.outlook.com include:_spf.atlassian.net ip4:10.129.124.8 ip4:10.129.127.2 ip4:10.129.42.106 ~all" 
inlanefreight.htb. 604800 IN NS ns.inlanefreight.htb. 
app.inlanefreight.htb. 604800 IN A 10.129.18.15 
internal.inlanefreight.htb. 604800 IN A 10.129.1.6 
mail1.inlanefreight.htb. 604800 IN A 10.129.18.201 
ns.inlanefreight.htb. 604800 IN A 10.129.34.136 
inlanefreight.htb. 604800 IN SOA inlanefreight.htb. 
root.inlanefreight.htb. 2 604800 86400 2419200 604800
```
By looking at the A record we discover multiple link domain name to direct ip address

From here we can try do Zone Transfer to any one of these to enumerate more.