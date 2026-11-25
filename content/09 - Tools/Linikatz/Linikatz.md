- Linux version of Mimikatz, needs root
- Pulls credentials/tickets from whatever Kerberos/AD integration is in use (sssd, FreeIPA, Samba, Vintella, etc), all in one run

```bash
/opt/linikatz.sh
```
- Dumps results in ccache/keytab format, use the same way as any other found ticket (see [[Pass the Ticket (Linux)]])