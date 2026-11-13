
Nmap commonly reports 6 port states:

| State | Meaning | What Nmap observed | What it means for pentesting |
|---|---|---|---|
| `open` | A service is listening | Nmap received a response indicating the port is accepting connections | **Highest priority** — enumerate the service |
| `closed` | No service is listening | Target is reachable but rejected the connection | Usually low priority, but confirms the port is reachable |
| `filtered` | Nmap cannot determine the state | Firewall/filter prevented Nmap from determining whether the port is open | Investigate firewall/filtering if relevant |
| `unfiltered` | Port is reachable, but Nmap can't determine open/closed | Packets reached the port, but response doesn't establish whether a service is listening | Usually seen with ACK scans |
| `open\|filtered` | Could be open or filtered | Nmap cannot distinguish between the two | Common with UDP and some stealth scans |
| `closed\|filtered` | Could be closed or filtered | Nmap cannot distinguish between the two | Mainly associated with certain scan types |
