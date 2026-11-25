- Auto-extracts creds from live traffic or a pcap, so we don't have to manually filter in Wireshark

```bash
./Pcredz -f capture.pcapng -t -v
```
- Pulls: FTP/POP/IMAP/SMTP creds, SNMP community strings, HTTP Basic/NTLM/Form creds, NTLMv1/v2 hashes, Kerberos pre-auth hashes, credit card numbers
- Needs its own dependencies, easiest to run via their Docker container