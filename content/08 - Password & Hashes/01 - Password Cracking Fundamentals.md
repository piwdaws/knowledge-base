- Passwords are usually not stored as plain text, they are stored as a hash
- A hash is a one way function, same input always gives the same output, but we can't reverse the hash back to the password

---

- Password cracking means guessing a password, hashing the guess, and checking if it matches the stored hash
- Three ways to do this: rainbow table, dictionary attack, brute force

---
## Rainbow Tables
- A rainbow table is a pre-made list of password -> hash, already calculated
- If the hash we have is in the table, we instantly know the password
- Downside, the table only works for hashes that were never salted

---
## Salting
- A salt is a random string added to the password before hashing
- Same password + different salt = different hash
- Salt is not secret, it's stored together with the hash (usually in front of it), the system needs it to check the login later
- Why this breaks rainbow tables: the table was pre-made for password only, not password+salt, so our hash won't match anything in the table anymore.

```bash
# password: Soccer06! salt: Th1sIsTh3S@lt_ 
echo -n Th1sIsTh3S@lt_Soccer06! | md5sum
```
---

## Dictionary Attack
- Instead of guessing random characters, we use a wordlist of real/common passwords and try each one
- This is the one we use most as pentester, because we are usually under time pressure
- `rockyou.txt` is the most common wordlist, it's 14 million real passwords leaked from a real website hack in 2009

---
## Brute Force
- Try every possible combination of characters until one matches
- This WILL eventually crack any password, but can take forever on long/strong passwords
- Only realistic for short passwords (under 9 characters) 
- Rarely used directly, mask attack (see Hashcat note) is the smarter version of this

---
## Why Custom Wordlists Work Better
- Rockyou.txt is generic, real people have personal passwords
- Most people base their password on something personal: pet name, company name, hobby, birth year, kid's name
- Basic OSINT (digging up info about the target person/company) + a mutation rule = way better wordlist than rockyou alone
- Common password pattern to fit policy requirements: `Word` -> `Word123` -> `Word2024` -> `Word2024!` -> `P@ssw0rd2024!`
- If org forces password change regularly, people usually just change 1 small thing (month name, last digit)