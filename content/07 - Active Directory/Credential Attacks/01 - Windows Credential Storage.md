- Windows caches/stores credentials in a few places, each one is a different attack target

## How login actually works (the flow)
1. We type username/password at the login screen (LogonUI)
2. WinLogon grabs that input and hands it to LSASS
3. LSASS checks it against either SAM (if local account) or Active Directory (if domain account)
4. If correct, LSASS caches the credential in memory for as long as we're logged in

This matters because it tells us **where** to look depending on what kind of access we have:
- Already logged in as someone? -> their creds are sitting in LSASS memory right now
- Have admin on the machine? -> SAM file has every local account's hash
- Have admin on the Domain Controller? -> NTDS.dit has every domain account's hash

## LSASS (lsass.exe)
- The process that does the actual auth checking, and caches logged-in users' creds in memory (hashes, sometimes Kerberos tickets, rarely cleartext)
- This is why dumping LSASS memory is so valuable, it shows us who's currently logged in and what they typed to get in

## SAM database
- Stores LOCAL user password hashes only (accounts that exist on just that one machine, not domain accounts)
- Location: `%SystemRoot%\system32\config\SAM`
- Needs SYSTEM-level access to even read it, that's why we need admin first
- A separate file called `SYSTEM` holds the "boot key" used to decrypt SAM, we need to grab both together or SAM is useless to us

## NTDS.dit
- Same idea as SAM but for an entire AD domain, lives only on Domain Controllers
- Location: `%systemroot%\NTDS\ntds.dit`
- Compromising this = compromising every single account in the domain, not just one PC
- A machine joined to a domain stops checking its own SAM for login, it asks the DC instead — but the SAM file is still there and local accounts on it (e.g. `.\Administrator`) still work if we have physical/direct access

## Credential Manager
- Lets users/apps save creds for OTHER systems and sites (RDP, mapped drives, websites) so you don't retype them
- Stored encrypted under the user's own profile, so we need access as that user (or need to decrypt it with something like Mimikatz) to get the password back out

See: [[02 - Attacking SAM]] · [[03 - Attacking LSASS]] · [[06 - Attacking Active Directory and NTDS]] · [[04 - Attacking Credential Manager]] · [[05 - Credential Hunting]]