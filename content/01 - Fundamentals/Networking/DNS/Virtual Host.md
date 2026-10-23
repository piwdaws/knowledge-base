## What is Virtual host
-  Configuration method that allows a single web server to host and serve **multiple websites or domain names** simultaneously
- Means 1 Ip Address can contain more than 1 service
- The way they decide which service we can go they either:
- Look at the port we requesting
- Or they look at the Host Header

---
## Example Host Header
```http
GET /index.html HTTP/1.1
Host: ://mysite.com
```
- It look at the Host Header on what our request is

---
## Diagram VHost

![[Screenshot 2026-09-17 at 3.03.15 PM.png]]

---
