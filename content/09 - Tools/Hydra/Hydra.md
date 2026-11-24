- Online login brute force tool, works across many protocols (ssh, rdp, smb, ftp, http, etc)

```bash
hydra -L user.list -P password.list <protocol>://<target-IP>   # userlist + passlist
hydra -C user_pass.list <protocol>://<target-IP>                # combo list (user:pass pairs = credential stuffing)
```
- `-t` to control threads, lower it for picky services (RDP, SMB don't like too many parallel connections)
- Known issue: older hydra breaks on SMBv3 ("invalid reply from target"), use NetExec or Metasploit `smb_login` instead