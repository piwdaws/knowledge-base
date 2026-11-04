## Overview
- A limited shell may provide command execution without a fully interactive terminal. 
- This can happen after obtaining a shell through a remote service or an application.

---
## Spawn with Python
- We can spawn one using the Python module if its present in the system
- You can check what Python exist by using `which python`

```bash
# Python 3
python3 -c 'import pty; pty.spawn("/bin/bash")'

# Python 2
python = -c 'import pty; pty.spawn("/bin/bash")'
```
---
## Spawn a shell with /bin/sh
- Interactive mode
```bash
/bin/sh -i 
sh: no job control in this shell 
sh-4.2$
```

---
## Perl
- Perl can execute another program through its exec function
```perl
perl -e 'exec "/bin/sh";'
```

---
## Ruby
```ruby
ruby -e 'exec "/bin/bash"'
```
---
## Lua
```lua
os.execute('/bin/sh')
```

---
## AWK
```bash
awk 'BEGIN {system("/bin/sh")}'
```

---

## Using Exec to launch a shell
- Basically we search for the /bin/sh and execute it

```bash
find . -exec /bin/sh \; -quit
```
- `.` — search from the current directory.
- `-exec` — execute the specified command.
- `/bin/sh` — the command to execute.
- `\;` — terminates the `-exec` command specification.
- `-quit` — stops the search after the first successful match.

---
## Execute AWK through find
```bash
find . -exec /bin/awk 'BEGIN {system("/bin/sh")}' \; -quit
```

---
## Using VIM
- Launch vim to shell
```bash
vim -c ':!/bin/sh'
```

- Configure and launch shell from within VIM
```bash
:set shell=/bin/sh 
:shell
```

---

## Execution Permission Consideration
- It possible to run as root a program SUID Executable is set to root
```bash
# We know the owner of this file is root
# The owner part of rws got s on it. Mean the SUID Executable is set to the owner which is root
# Mean any user runs this program, it executes with the Effective user ID in this case root rather than the user who launched it
-rwsr-xr-x 1 root root 1200 program
```


- Another way would be by using sudo -l to check whether we can execute command as root
```bash
sudo -l
Matching Defaults entries for apache on ILF-WebSrv:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User apache may run the following commands on ILF-WebSrv:
    (ALL : ALL) NOPASSWD: ALL
```
- Here some breakdown:
	- (ALL : ALL) : This allow us to run as any user and group. That include root
	- NOPASSWD: Normally sudo would ask pass. But this will remove that
	- ALL : means any command is ok.