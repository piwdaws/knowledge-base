## Overview
- **CMD (**`cmd.exe`**):** The traditional Windows command interpreter.
- **PowerShell:** A shell and scripting environment that supports cmdlets and .NET objects.

---
## CMD vs PowerShell

| Characteristic | CMD                                                        | PowerShell                                                           |
| -------------- | ---------------------------------------------------------- | -------------------------------------------------------------------- |
| Main purpose   | Traditional command-line interaction                       | Command-line interaction and automation                              |
| Commands       | Traditional Windows commands and utilities                 | Cmdlets, scripts and many familiar Windows commands                  |
| Data handling  | Primarily text input and output                            | Supports structured .NET objects                                     |
| Automation     | Batch files, commonly `.bat`                               | PowerShell scripts and reusable modules                              |
| Compatibility  | May be available on older Windows systems                  | Availability depends on the installed Windows/PowerShell version     |
| Considerations | Limited compared with PowerShell for structured automation | Script execution policies and security controls may affect execution |

---

## When Each Shell is useful

### CMD
- Only simple command-line interaction is required.
- Traditional Windows commands or batch files are needed.
- The host is old and PowerShell may not be available.
- PowerShell-specific requirements prevent a script from running.
### PowerShell
- Cmdlets or custom scripts are required.
- Structured .NET objects are useful.
- Automation needs more functionality than a basic command interpreter provides.
- PowerShell-specific modules or aliases are required.

---

## Related Topic
[[01 - Anatomy of a Shell]]
[[Living Off The Land]]
[[Windows Payload]]
[[01 - Metasploit Framework]]


