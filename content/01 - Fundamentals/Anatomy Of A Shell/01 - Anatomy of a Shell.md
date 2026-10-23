## Overview
- A shell is a program that interprets user commands and allows interaction with an operating system. 
- It can be used to manage files, execute programs, administer systems, automate tasks, and interact with remote machines.

A command-line environment typically involves three components:
1. **Operating system:** Manages system resources, processes, memory, files, and hardware.
2. **Terminal emulator:** Provides a text-based interface for interacting with a shell.
3. **Shell / command interpreter:** Parses commands and runs programs or built-in instructions.

---
## Terminal Emulator
- A terminal emulator is an application that provides a terminal interface. It does not necessarily interpret commands itself; it launches or connects to a shell.

- Examples:

| Operating system | Terminal emulators                            |
| ---------------- | --------------------------------------------- |
| Windows          | Windows Terminal, PuTTY, Cmder                |
| Linux            | GNOME Terminal, MATE Terminal, Konsole, xterm |
| macOS            | Terminal, iTerm2                              |
| Cross-platform   | kitty, Alacritty                              |

----

## Command Language Interpreters
- A command language interpreter processes commands entered by a user. Different shells support different syntax, built-in commands, scripting features, and environment variables.
### Bash
- Bash (Bourne Again SHell) is widely used on Linux systems.

```bash
whoami
pwd
ls -la
```
### PowerShell
- PowerShell is a command-line shell and scripting language used for Windows administration and available on other platforms.

```Powershell
whoami
Get-Location
Get-ChildItem
```

---

## Identifying the Active Shell
### Using PS
- On Linux, ps command display process information
```bash
ps

PID   TTY      TIME     CMD
4232  pts/1    00:00:00 bash
11435 pts/1    00:00:00 ps
```
### Using SHELL
- This environment variable commonly identifies the user's configured login shell.
```bash
echo "$SHELL"
/bin/bash
```
### Using env
- This displays environment variables available to the process. Look for variables such as `SHELL`, but interpret them carefully because their values depend on the environment.
```bash
env
```
---
## Related stuff
[[Bind Shell]]
[[Reverse Shell]]
