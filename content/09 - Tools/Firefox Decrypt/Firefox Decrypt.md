- Decrypts saved Firefox logins (stored encrypted in `logins.json` inside the user's firefox profile folder)

```bash
python3.9 firefox_decrypt.py
```
- Picks the Firefox profile, then prints out each saved site + username + password in cleartext
- LaZagne's `browsers` module does this automatically too, use firefox_decrypt directly if we only care about Firefox or LaZagne fails for some reason