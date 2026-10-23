Server Message Block (SMB) regulates access to file and entire directories on another network resources such as printer, router for the network.

---

## Listing Publicly Visible Share

```bash
# List server anonymously
smbclient -N -L //192.168.10.1

# List using credential 
smbclient -L //192.168.10.1 -U username%password

# List if server belong to Active Directory or Corporate server
smbclient -L //192.168.10.1 -U username -W DOMAIN NAME
```

---
## Connecting to a Share
```bash
smbclient //192.168.10.1/SHARENAME
```
