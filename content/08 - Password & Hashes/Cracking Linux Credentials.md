- Once we have root, we can grab passwd + shadow and crack the hashes offline

---
## Steps
```bash
cp /etc/passwd /tmp/passwd.bak
cp /etc/shadow /tmp/shadow.bak
unshadow /tmp/passwd.bak /tmp/shadow.bak > /tmp/unshadowed.hashes
```
- `unshadow` (comes with John) merges both files into 1 crackable file

```bash
hashcat -m 1800 -a 0 /tmp/unshadowed.hashes rockyou.txt -o /tmp/unshadowed.cracked
```
- `-m 1800` = sha512crypt (the common Linux hash type), check the hash's `$id$` to confirm the right mode

- This is literally the exact use case [[John The Ripper]]'s single crack mode was built for, since it guesses based on username/home dir info already sitting in the unshadowed file

