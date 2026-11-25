- Scans SMB shares for files matching a content string, run from Linux, no need to be domain-joined

```bash
docker run --rm -v ./manspider:/root/.manspider blacklanternsecurity/manspider <ip> -c 'passw' -u 'user' -p 'pass'
```
- `-c` = the string to search inside file contents