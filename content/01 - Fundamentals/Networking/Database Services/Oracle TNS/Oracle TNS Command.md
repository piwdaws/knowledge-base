
## Some important command
```sql
SELECT user FROM dual;

SELECT banner FROM v$version;

SELECT name FROM v$database;

SELECT table_name FROM all_tables;

SELECT table_name FROM user_tables;

SELECT username FROM all_users;

SELECT * FROM user_role_privs;

SELECT * FROM user_sys_privs;

SELECT * FROM <table>;

-- Dumping password hashes
SELECT name, password FROM sys.user$;
```

## Command Reference

| Category                | Command                                                               | What it does                               |
| ----------------------- | --------------------------------------------------------------------- | ------------------------------------------ |
| **Connection**          | `sqlplus <user>/<password>@<IP>/<SID>`                                | Connect to Oracle database                 |
| **Database**            | `SELECT name FROM v$database;`                                        | Show database name                         |
| **Version**             | `SELECT banner FROM v$version;`                                       | Show Oracle version information            |
| **Current User**        | `SELECT user FROM dual;`                                              | Show currently authenticated Oracle user   |
| **Tables**              | `SELECT table_name FROM all_tables;`                                  | List tables accessible to the current user |
| **Own Tables**          | `SELECT table_name FROM user_tables;`                                 | List tables owned by current user          |
| **Columns**             | `SELECT column_name FROM all_tab_columns WHERE table_name='<TABLE>';` | Show columns for a table                   |
| **Read Data**           | `SELECT * FROM <table>;`                                              | Dump all rows from a table                 |
| **Filter Data**         | `SELECT * FROM <table> WHERE <column>='<value>';`                     | Search/filter table data                   |
| **Users**               | `SELECT username FROM all_users;`                                     | List database users                        |
| **Privileges**          | `SELECT * FROM user_role_privs;`                                      | Show roles granted to current user         |
| **System Privileges**   | `SELECT * FROM user_sys_privs;`                                       | Show system privileges                     |
| **Table Privileges**    | `SELECT * FROM user_tab_privs;`                                       | Show privileges on tables                  |
| **Current Schema**      | `SELECT SYS_CONTEXT('USERENV','CURRENT_SCHEMA') FROM dual;`           | Show current schema                        |
| **Databases/Instances** | `SELECT instance_name FROM v$instance;`                               | Show Oracle instance name                  |
| **Exit**                | `EXIT;`                                                               | Leave SQL*Plus                             |

---
## Some Oracle Specific command
```sql
SELECT * FROM dual;
```
- dual is like a blank notepad
- In Oracle, every SELECT need to have FROM
- So we use dual an empty permanent tiny table

```sql
-- Example Usage
SELECT user FROM dual;
SELECT SYSDATE FROM dual;
SELECT banner FROM v$version;
```