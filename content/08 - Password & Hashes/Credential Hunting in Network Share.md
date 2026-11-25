- Company network shares (file servers) often have creds left behind in config files, scripts, old backups, unattend.xml, etc
- Same keyword idea as host-based hunting (`passw`, `user`, `token`, `key`, `secret`, plus company-specific terms like `INLANEFREIGHT\` or a non-English word if the target isn't English-speaking)
- Be picky about which shares to scan, IT/Finance shares are more likely to have something than a "company photos" share, and scanning everything takes forever

---
## From Windows, domain-joined: Snaffler
- Auto-discovers accessible shares on the domain and searches them for interesting files

```cmd
Snaffler.exe -s
```
- `-u` = also pull AD usernames and search for references to them in files
- `-i` / `-n` = include/exclude specific shares
- Expect a lot of noise/false positives, manual review of the results is still needed

---
## From Linux: MANSPIDER
- Scans SMB shares remotely for files matching a content string, don't need to be on a domain-joined machine

```bash
docker run --rm -v ./manspider:/root/.manspider blacklanternsecurity/manspider 10.129.234.121 -c 'passw' -u 'user' -p 'pass'
```
- `-c` = content string to search for inside files

---
## NetExec (cross-platform, already have it set up)
```bash
nxc smb <ip> -u user -p pass --spider <share> --content --pattern "passw"
```
- good option if we already have nxc running and don't want to add another tool