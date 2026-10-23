## Overview
- You can guess a remote system's operating system by running a `ping` command and checking the **Time to Live (TTL)** value in the response.

---
## Pinged Host
```bash
piwpiw95@htb[/htb]$ ping 192.168.86.39 

PING 192.168.86.39 (192.168.86.39): 56 data bytes 
64 bytes from 192.168.86.39: icmp_seq=0 ttl=128 time=102.920 ms 
64 bytes from 192.168.86.39: icmp_seq=1 ttl=128 time=9.164 ms 
64 bytes from 192.168.86.39: icmp_seq=2 ttl=128 time=14.223 ms 
64 bytes from 192.168.86.39: icmp_seq=3 ttl=128 time=11.265 ms
```

---

## Default Starting TTL values

- **64**: Linux, macOS, Android, and other Unix-like systems
- **128**: Windows systems
- **255**: Network equipment like routers, switches, and many IoT devices

### Know that this a rough passive estimate. Firewall, VPN or other stuff can modify or obscure it


---

## Related Topic

[[Banner Grabbing]]
[[SMB Enumeration]]


