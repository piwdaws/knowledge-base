- Same cracking idea, but for password-protected archives (zip, rar, 7z) and encrypted drives (bitlocker)

---
## ZIP
```bash
zip2john ZIP.zip > zip.hash
john --wordlist=rockyou.txt zip.hash
john zip.hash --show
```

---
## OpenSSL Encrypted Files (e.g. a .gzip made with openssl)
- Check the real file type first, extension can lie

```bash
file GZIP.gzip
# GZIP.gzip: openssl enc'd data with salted password
```

- No `2john` script for this one, so we just brute force it directly with openssl in a loop, only the correct password will successfully decrypt+extract

```bash
for i in $(cat rockyou.txt); do openssl enc -aes-256-cbc -d -in GZIP.gzip -k $i 2>/dev/null | tar xz; done
```

- Ignore the gzip/tar error spam, just check the folder after, if a new file appeared, that was the password

---
## BitLocker (Windows full-disk encryption)
- Get 4 hashes from the encrypted drive, we only care about the 1st one (`$bitlocker$0$...`), that's the password hash. the other 3 are for the 48-digit recovery key, not practical to brute force

```bash
bitlocker2john -i Backup.vhd > backup.hashes
grep "bitlocker\$0" backup.hashes > backup.hash
hashcat -a 0 -m 22100 backup.hash /usr/share/wordlists/rockyou.txt
```

- Mount on Linux/macOS with `dislocker`, once we have the password

```bash
sudo losetup -f -P Backup.vhd
sudo dislocker /dev/loop0p2 -u<password> -- /media/bitlocker
sudo mount -o loop /media/bitlocker/dislocker-file /media/bitlockermount
```