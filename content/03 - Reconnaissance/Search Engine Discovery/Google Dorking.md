It can be used during reconnaissance to discover publicly accessible: 
- Login pages 
- Administrative interfaces 
- Documents 
- Configuration-related files 
- Backup files 
- Other potentially sensitive information

We use [[Search Operators]] to Google Dorking

---
## Example

```bash
# Login Pages
site:example.com inurl:login
site:example.com (inurl:login OR inurl:admin)
```
```bash
# Exposed Document
site:example.com filetype:pdf
site:example.com (filetype:xls OR filetype:docx)
```
```bash
# Configuration Files
site:example.com inurl:config.php
site:example.com (ext:conf OR ext:cnf)
```
```bash
# Databases Backup
site:example.com inurl:backup
site:example.com filetype:sql
```
