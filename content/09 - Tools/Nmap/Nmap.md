## Overview

Network Mapper (`Nmap`) is an open-source network analysis and security auditing tool written in C, C++, Python, and Lua. 

Designed to scan networks and identify which hosts are available on the network using raw packets, and services and applications, including the name and version, where possible. 

Can identify the operating systems and versions of these hosts. 

Besides other features, Nmap also offers scanning capabilities that can determine if packet filters, firewalls, or intrusion detection systems (IDS) are configured as needed.

---
## Basic Syntax

``` Bash
piwpiw95@htb[/htb]$ nmap <scan types> <options> <target>
```

## Target Specification

| Option          | Description                    | Syntax                                         |
| --------------- | ------------------------------ | ---------------------------------------------- |
| `-iL`           | Scan targets from a file       | `nmap -iL targets.txt`                         |
| `-iR`           | Scan random targets            | `nmap -iR 10`                                  |
| `--exclude`     | Exclude specific hosts         | `nmap 10.10.10.0/24 --exclude 10.10.10.5`      |
| `--excludefile` | Exclude hosts listed in a file | `nmap 10.10.10.0/24 --excludefile exclude.txt` |

---
## Host Discover
```Bash
nmap -sn 10.10.10.0/24
```
- Useful for finding which host alive
- Discover live host without performing port scan
- Useful if you want to scan entire subnet

## Skip Host Discovery
```bash
nmap -Pn 10.10.10.10
```
- Treat all hosts as online and scan them.
- Useful when ICMP/ping is blocked.
- Nmap say its down but you know the host exist

---
## ICMP Echo Request
```bash
nmap -PE 10.10.10.10
```
- Use ICMP Echo requests for host discovery.

## ICMP Timestamp Request
```bash
nmap -PP 10.10.10.10
```
- Use ICMP Timestamp requests for host discovery.

## TCP ACK Ping
```bash
nmap -PA 80,443 10.10.10.10
```
- Send TCP ACK packets to specified ports.
- Useful when scan through certain firewall config

## UDP Ping
```bash
nmap -PU 53 10.10.10.10
```
- Send UDP packets for host discovery.
- Useful when TCP/ICMP discovery not give useful result

---
## Port Scanning 
```bash
nmap -p 22 10.10.10.10
nmap -p 22,80,443 10.10.10.10
nmap -p 1-1000 10.10.10.10
```
- Scan Specific Port
- Incase want to scan all port use -**p**-

---
## Scan Type

### TCP SYN Scan
```bash
sudo nmap -sS 10.10.10.10
```
- Default TCP scan when running with sufficient privileges.
- Perform TCP SYN scan without completing full TCP Connection
- Useful TCP scans for normal enumeration
- Most useful TCP scan for normal enumeration

### TCP Connect Scan
```bash
nmap -sT 10.10.10.10
```
- Complete the TCP connection using the OS networking stack.
- If you dont have privilege for -sS
- Normal TCP scan

### UDP Scan
```bash
sudo nmap -sU 10.10.10.10
```
- Useful When you want to discover UDP services

### TCP ACK Scan
```bash
sudo nmap -sA 10.10.10.10
```
- Use to determine whether ports are filtered by firewall

### TCP Null Scan 
```bash
sudo nmap -sN 10.10.10.10
```
- Send the TCP Packet with no flag sent
- Useful for firewall behaviour testing

### TCP FIN Scan
```bash
sudo nmap -sF 10.10.10.10
```
- Useful for test how target handle unusual TCP packets

### TCP Xmas Scan
```bash
sudo nmap -sX 10.10.10.10
```
- Set FIN, PSH and URG flags.
- Firewall testing

---

## Service & Enumeration
```bash
nmap -sV 10.10.10.10
```
- Determine service and version running in open port

## Default NSE Script
```bash
nmap -sC 10.10.10.10
```
- Run nmap default NSE Script

##  OS Detection
```bash
sudo nmap -O 10.10.10.10
```
- Attempt to determine target OS

---

## OS Aggressive Scan 
```bash
sudo nmap -O --osscan-guess 10.10.10.10
```

## Agressive Scan
```bash
nmap -A 10.10.10.10
```
Enabled Several detection feature
- OS Detection
- Version Detection
- Default NSE Script
- Traceroute

---

## Nmap Scripting Engine
```bash
nmap --script <script> <target>
```
- Run specific NSE Script 

```bash
nmap --script <category> <target>
```
- Run a script category

### Common Category
```bash
auth
broadcast
brute
default
discovery
dos
exploit
external
intrusive
malware
safe
version
vuln
```

---
### Timing & Performance
```bash
nmap -T4 10.10.10.10
```

| Timing | Description                     |
| ------ | ------------------------------- |
| `-T0`  | Paranoid — extremely slow       |
| `-T1`  | Sneaky — very slow              |
| `-T2`  | Polite — slower, less bandwidth |
| `-T3`  | Normal — default                |
| `-T4`  | Aggressive — faster             |
| `-T5`  | Insane — extremely fast         |

## Set Min & Max Packet Transfer Rate
```bash
nmap --min-rate 1000 10.10.10.10

nmap --max-rate 100 10.10.10.10
```

---
## Firewall / Evasion Option

### Fragments IP Packets
```bash
sudo nmap -f 10.10.10.10
```

### Decoy IP Addr during scanning
```bash
sudo nmap -D RND:5 10.10.10.10
```

### Spoof Source IP
```bash
sudo nmap -S 10.10.10.20 10.10.10.10
```

### Specify Network Interface
```bash
sudo nmap -e eth0 10.10.10.10
```

---
## Output

### Save Output as Readable Text
```bash
nmap -oN scan.txt 10.10.10.10
```

### XML Output
```bash
nmap -oX scan.xml 10.10.10.10
```

### Grep-Friendly format
```bash
nmap -oG scan.txt 10.10.10.10
```

### Save as All Format
```bash
nmap -oA scan 10.10.10.10
```

---
## Verbosity & Debugging

```bash
# Verbosity 
nmap -v 10.10.10.10

# Inc verbosity
nmap -vv 10.10.10.10

# Enabled Debugging
nmap -d 10.10.10.10
```

---
## Miscellaneous Option
```bash
# Enabled DNS Resolution
nmap -n 10.10.10.10

# Always Perform DNS Resolution
nmap -R 10.10.10.10

# Show why nmap said some port in particular state
nmap --reason 10.10.10.10

# Only show Open Port
nmap --open 10.10.10.10

# Scan using IPv6
nmap -6 2001:db8::1

```

