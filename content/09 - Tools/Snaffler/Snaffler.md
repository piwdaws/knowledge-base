- Run on a domain-joined Windows machine, auto-finds accessible network shares and flags interesting files inside them (passwords, keys, configs)

```cmd
Snaffler.exe -s
```
- `-u` = pull AD users, search file contents for references to them
- `-i SHARE1,SHARE2` / `-n SHARE1,SHARE2` = only include / exclude specific shares
- Output is noisy, expect to manually sort real hits from false positives