rpcclient offer many different requests with which we can execute specific functions on the SMB server to get information.

---
## Connect anonymously
```bash
rpcclient -U "" //192.168.10.1
```

---

## Some Useful Command

| Command | Subsystem | Description |
| :--- | :--- | :--- |
| **`srvinfo`** | Server | Queries server information (OS version, server type). |
| **`netshareenumall`** | Shares | Lists all available network shares, including hidden ones. |
| **`netsharegetinfo <share>`** | Shares | Displays detailed information and permissions for a specific share. |
| **`enumalsgroups <domain/builtin>`**| Groups | Lists all alias/local groups (e.g., Administrators, Users). |
| **`enumdomgroups`** | Groups | Lists all domain groups. |
| **`querygroup <rid>`** | Groups | Shows details and membership information for a specific group RID. |
| **`enumdomusers`** | Users | Lists all user accounts present on the target machine. |
| **`queryuser <rid/username>`** | Users | Retrieves detailed information for a specific user (password age, login count). |
| **`lookupnames <username>`** | SID/Name | Resolves a username to its corresponding Security Identifier (SID). |
| **`lookupsids <sid>`** | SID/Name | Performs reverse lookup to resolve a SID back to a username. |
| **`lsaquery`** | LSA | Queries the Local Security Authority policy (reveals Domain SID). |
| **`dsrolegetprimarydomaininfo`** | Domain | Identifies the domain name and whether the machine is a Domain Controller. |
| **`getdriver <printername>`** | Printing | Retrieves printer driver information (useful for print spooler exploits). |

---
## Example queryuser

![[Screenshot 2026-09-13 at 12.15.18 AM.png]]