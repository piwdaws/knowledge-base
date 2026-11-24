- Besides login hashes, we can also crack password-protected files (ssh key, office doc, pdf)
- Same idea as before: convert file -> hash -> crack hash with john/hashcat

---
## Finding Encrypted Files
- Search for common encrypted file extensions

```bash
find / -name "*.pdf" 2>/dev/null
```

- SSH keys don't have a fixed extension, but always start with a fixed header, so grep for that instead

```bash
grep -rnE '^\-{5}BEGIN [A-Z0-9]+ PRIVATE KEY\-{5}$' /* 2>/dev/null
```

- To check if a found SSH key needs a passphrase, try reading it

```bash
ssh-keygen -yf id_rsa
# if it asks "Enter passphrase for...", it's protected
```

## Cracking Steps (same pattern every time)
1. Convert file to a hash with the matching `*2john` script
2. Run john or hashcat on that hash file

```bash
ssh2john.py id_rsa > ssh.hash
office2john.py Protected.docx > doc.hash
pdf2john.py file.pdf > pdf.hash

john --wordlist=rockyou.txt ssh.hash
john ssh.hash --show
```

See [[John The Ripper]] for the full list of `2john` tools and how to find one for a file type.