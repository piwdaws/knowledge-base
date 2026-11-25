- Linux handles login through PAM (Pluggable Authentication Modules), it reads/writes `/etc/passwd` and `/etc/shadow`

---
## /etc/passwd
- Readable by everyone, has 1 line per user, 7 fields separated by `:`
- Example
	- htb-student:x:1000:1000:,,,:/home/htb-student:/bin/bash
	- username : password : UID : GID : GECOS(full name etc) : home dir : shell

- Password field is almost always `x`, meaning the real hash is in `/etc/shadow` instead
- **If this field is EMPTY instead of `x`**, that means no password is needed, `su` would log straight in as that user with no prompt. Worth checking if this file is writable by us, since we could delete the `x` ourselves for root

---
## /etc/shadow
- Only readable by root, has the actual password hash, 9 fields
- Example
	- htb-student:$y$j9T$3QSBB6CbHEu...SNIP...f8Ms:18955:0:99999:7:::
	- username : hash : last changed : min age : max age : warn period : ...

- Hash format: `$<id>$<salt>$<hash>`, the id tells us the algorithm

| id  | algorithm                          |
| --- | ---------------------------------- |
| 1   | MD5                                |
| 5   | SHA-256                            |
| 6   | SHA-512                            |
| y   | Yescrypt (default on newer Debian) |

- If password field is `!` or `*` or empty, no Unix password login (but Kerberos/SSH key login might still work)

---
## /etc/security/opasswd
- Stores OLD password hashes, so the system can stop people reusing them
- Needs root to read
- Useful to us: if an old hash here is weak (MD5) even though current hash is strong, we can crack the old one and guess the user reused a similar password for their current one