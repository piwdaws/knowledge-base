## Password Spraying
- Instead of trying many passwords on 1 user, we try ONE password across MANY users
- Good when we suspect a default/common password was set company-wide (e.g. new hires all get `ChangeMe123!`)
- Avoids account lockout better than normal brute force, since each user only gets 1 attempt

```bash
netexec smb 10.100.38.0/24 -u usernames.list -p 'ChangeMe123!'
```

---
## Credential Stuffing
- Using leaked username:password pairs (from a data breach) against a different service
- Works because people reuse the same password everywhere

```bash
hydra -C user_pass.list ssh://10.100.38.23
```
- `-C` = combo file (user:pass pairs, not 2 separate lists)

---
## Default Credentials
- Routers, IoT, databases often still use factory default login
- Use `defaultcreds-cheat-sheet` tool to look these up fast instead of googling one by one

```bash
pip3 install defaultcreds-cheat-sheet
creds search <vendor/product>
```
- Also worth checking the product's own documentation/manual, sometimes faster than searching