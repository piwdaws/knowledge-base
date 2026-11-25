- After landing a shell, search the system for creds BEFORE trying heavier privesc, this is often the fastest win
- 4 places to check: files, history, memory, keyrings/browser

---
## Files
Search by common config extensions, then grep inside them for keywords

```bash
find / -name "*.conf" -o -name "*.config" -o -name "*.cnf" 2>/dev/null
grep -ril "user\|password\|pass" /etc/mysql/ 2>/dev/null
```
- Also check: databases (`.sql .db`), notes (`.txt` or no extension at all), scripts (`.py .sh .pl`), cronjobs (`/etc/crontab`, `/etc/cron.d/`)
- Scripts and cronjobs are good targets because they often need to auto-login without a human typing a password each time

---
## History
```bash
cat ~/.bash_history
```
- People sometimes type passwords directly into commands and forget it's logged, e.g. `/tmp/api.py cry0l1t3 6mX4UP1eWH3HXK`

---
## Logs
- Worth a quick look, but don't read every log manually, grep for auth-related keywords instead

```bash
grep -i "accepted\|failed\|password\|sudo" /var/log/auth.log 2>/dev/null
```
- `/var/log/auth.log` (Debian) or `/var/log/secure` (RedHat) are the main ones for login activity

---
## Memory / Keyrings / Browser
- [[Mimipenguin]] - dumps logged-in user creds from memory, needs root
- [[LaZagne]] - way broader, pulls from browsers, wifi, git, ssh, keepass, etc, needs root too
- Browser creds specifically (Firefox) are encrypted in `logins.json`, decrypt with [[Firefox Decrypt]] or let LaZagne handle it directly

See also: [[05 - Credential Hunting]] (Windows version) for the same idea on a Windows box

---

See also: [[Credential Hunting in Network Traffic]] · [[Credential Hunting in Network Share]] for hunting beyond the local machine