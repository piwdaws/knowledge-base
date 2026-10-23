- We grab the introduction text or welcome text presented by the web server or Services
- Example:
	- When we SSH, it show the SSH version
	- Look at the response header of a webpage

---
## Easy way for Banner Grabbing
```bash
# -I is used to fetch only the HTTP header
curl -I https://example.com
```
```bash
# Example Output
HTTP/1.1 301 Moved Permanently
Server: Apache/2.4.41 (Ubuntu)
X-Powered-By: PHP/8.1.2
Location: https://www.target.com/
```
- From the output we discover that the page trying to redirect us to different Location
- We also discover the Web version and its OS
- Other than that we discover its PHP 