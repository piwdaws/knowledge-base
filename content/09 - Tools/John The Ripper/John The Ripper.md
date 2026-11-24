- John the Ripper (JtR / john) is a password cracking tool, support brute force and dictionary attack 
- Use the "jumbo" version, it has more features and support more hash types

---
## 3 Cracking modes

**Single crack mode**
- Best for cracking Linux user passwords 
- It guesses password based on the username, full name, home folder name (info already in `/etc/passwd`) 
- Example: user `r0lf` with full name `Rolf Sebastian` -> john will try things like `Rolf`, `Sebastian`, `r0lf1` etc
```bash
john --single passwd
```

**Wordlist mode**
- Normal dictionary attack, try every password in a wordlist file against the hash
```bash
john --wordlist=<wordlist_file> <hash_file>
```
- Can add `--rules` to apply transformations (capitalize, add number, etc) to each word in the list, this generates more guesses from the same wordlist

**Incremental mode**
- This is the brute force mode, tries every character combination 
- Smarter than a plain brute force because it uses a statistical model to guess likely combinations first
- Most exhaustive but also slowest mode
```bash
john --incremental <hash_file>
```

---

## Identifying Unknown Hash Format 
- Sometimes we get a hash and don't know what type it is 
- Use `hashid` to guess the format, add `-j` flag to get the matching JtR format name
```bash
hashid -j <hash>
```

---

## Cracking Files (not just plain hashes) 
- JtR can also crack password-protected files (zip, ssh key, pdf, etc), not just raw hashes 
- We first need to convert the file into a hash john can read, using a `*2john` tool 
- Format: `<tool> <file_to_crack> > file.hash` then run john normally on `file.hash`

```bash
# We turn the file into a hash before using the normal john to crack the pass
zip2john secret.zip > zip.hash
ssh2john id_rsa > ssh.hash
```

- To find the right tool for a file type: `locate *2john*`

---

## Viewing the password
```bash
john --show zip.hash
# we mention the file name to see the cracked pass
```

---
- See [[Cracking Protected Files]] and [[Cracking Protected Archives]] for ssh key, office doc, pdf, zip and bitlocker examples