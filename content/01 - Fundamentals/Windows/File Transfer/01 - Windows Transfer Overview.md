File transfer is commonly required during Windows enumeration, exploitation, post-exploitation, password cracking, analysis, and exfiltration.

The method chosen depends on:
- Available network connectivity
- Allowed outbound ports
- Available Windows utilities
- Whether authentication is required
- Whether writing to disk is acceptable
- File size / command-line length limitations

---
## Transfer Method

| Method | Typical Direction | Key Requirement |
| :--- | :--- | :--- |
| **Base64** | Windows ↔ Linux | Shell access; suitable for smaller files |
| **HTTP/HTTPS** | Download / Upload | Web connectivity |
| **SMB** | Download / Upload | TCP/445 connectivity |
| **FTP** | Download / Upload | FTP connectivity |
| **WebDAV** | Download / Upload | HTTP/HTTPS connectivity |

---
## Self Reference

Linux --> Windows means Windows download file from linux or Linux upload file to Windows

Windows --> Linux means Linux download file from Windows or Windows upload file to Linux