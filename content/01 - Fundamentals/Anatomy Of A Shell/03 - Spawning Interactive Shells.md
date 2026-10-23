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





