- CeWL scans a website and pulls out real words used on it, saves them as a wordlist
- Good for building a targeted wordlist for a specific company instead of using generic rockyou

```bash
cewl https://target-site.com -d 4 -m 6 --lowercase -w target.wordlist
```
- `-d` = how many links deep to crawl
- `-m` = minimum word length to keep
- `--lowercase` = save all words lowercase
- `-w` = output file

- Combine this wordlist with a hashcat rule (see [[Hashcat]]) for a wordlist that's actually targeted at the company/person