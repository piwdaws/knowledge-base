 - Hashcat is a password cracking tool, similar to John but with strong GPU support, so it's usually faster

---
## Syntax
```bash
hashcat -a <attack_mode> -m <hash_type_id> <hashes> [wordlist/mask/rule]
```
- `-a` = attack mode (0 = dictionary, 3 = mask/brute force) 
- `-m` = hash type id (0 = MD5, 100 = SHA1, 1400 = SHA256, ...) 
- to find the id for a hash, use `hashid -m <hash>`, it will suggest the matching hashcat mode

---

## Dictionary Attack (-a 0) 
- Same idea as John's wordlist mode, try every word in a wordlist against the hash

```bash
hashcat -a 0 -m 0 <hash> /usr/share/wordlists/rockyou.txt
```

- If wordlist alone doesn't crack it, add a rule file, this transforms each word before trying it (capitalize, add numbers, leetspeak, etc) 

```bash
hashcat -a 0 -m 0 <hash> /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule
```

---

## Mask Attack (-a 3) 
- Smarter brute force, we define the pattern of the password instead of trying everything blindly 
- Example: if we know password starts with 1 uppercase, then 4 lowercase, then 1 number, then 1 symbol -> mask = `?u?l?l?l?l?d?s`

| Symbol | Means            |
| ------ | ---------------- |
| `?l`   | a-z              |
| `?u`   | A-Z              |
| `?d`   | 0-9              |
| `?s`   | symbols          |
| `?a`   | all of the above |

```bash
hashcat -a 3 -m 0 <hash> '?u?l?l?l?l?d?s'
```

- Can also make custom charset with `-1 -2 -3 -4`, then use `?1 ?2 ?3 ?4` in the mask

---
## Custom Rules (mutate a wordlist)
- We can take a plain wordlist and mutate each word using rules (capitalize, replace letter with symbol, add number, etc), this makes way more guesses from the same base word

| Rule | Does |
|---|---|
| `:` | do nothing |
| `l` | lowercase everything |
| `u` | uppercase everything |
| `c` | capitalize first letter |
| `sXY` | replace all X with Y |
| `$!` | add `!` at the end |

- Rules go in a `.rule` file, one rule per line
- Apply the rule file to a wordlist and save output to a new file

```bash
hashcat --force password.list -r custom.rule --stdout | sort -u > mut_password.list

# Basically we force the password.list and apply the custom.rule
# and sort it and output it in a file 
```

```bash
# Example of custom rule
cat custom.rule

:
c
so0
c so0
sa@
c sa@
c sa@ so0
$!
$! c
$! so0
$! sa@
$! c so0
$! c sa@
$! so0 sa@
$! c so0 sa@
```
- `best64.rule` (comes with hashcat/john) is the most reliable ready-made ruleset
