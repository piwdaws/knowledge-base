- Not every service encrypts traffic, old/misconfigured/test systems sometimes still run plaintext protocols (HTTP, FTP, SNMP, POP3, IMAP, SMTP, LDAP)
- If we can capture/see that traffic, we can read creds straight out of it, no cracking needed

---
## Manually, with Wireshark
- Good filters for this:
- Example of filter
	- http.request.method == "POST" # POST = likely a login form submit  
	- http contains "passw" # search packet content for the word  
	- tcp.port == 80 # narrow to one port/protocol
- Or Edit > Find Packet, search for a string like `passw` manually
- Once we find a POST request, open the packet and check the form data for username/password fields in plaintext

---
## Automated, with Pcredz
- Scans a live interface or a pcap file, pulls out creds automatically instead of searching manually

```bash
./Pcredz -f demo.pcapng -t -v
```
- Picks up: FTP/POP/SMTP/IMAP creds, SNMP community strings, HTTP Basic/NTLM/Form creds, NTLMv1/v2 hashes (SMB/LDAP/MSSQL/RPC), Kerberos pre-auth hashes
- Way faster than manually filtering in Wireshark when we have a big capture, use Wireshark when we want to manually confirm/inspect one specific finding

See also: [[05 - Credential Hunting]] (host-based, Windows) · [[Credentials Hunting]] (host-based, Linux) for hunting on the system itself instead of over the wire