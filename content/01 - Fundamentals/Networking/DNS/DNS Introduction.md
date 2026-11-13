## What is DNS? 
- DNS (Domain Name System) translates domain names into IP addresses.
- Example : Example.com  ---> 10.192.168.0 

---
## DNS Resolution 
1. Client asks a recursive DNS resolver. 
2. Resolver checks its cache. 
3. If not cached, it queries the DNS hierarchy. 
4. Resolver obtains the authoritative answer. 
5. Result is returned to the client.

---
## Some Important Term
| Term                 | Meaning                                             |
| -------------------- | --------------------------------------------------- |
| Recursive Resolver   | Performs DNS lookups on behalf of clients           |
| Authoritative Server | Holds the authoritative DNS records                 |
| Nameserver           | Server responsible for DNS information              |
| Zone                 | Portion of DNS namespace managed by an organization |
