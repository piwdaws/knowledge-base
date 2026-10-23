## Some important Command
```sql
-- Who am I?
SELECT SYSTEM_USER;
SELECT USER_NAME();

-- What version?
SELECT @@VERSION;

-- What database am I in?
SELECT DB_NAME();

-- Am I sysadmin?
SELECT IS_SRVROLEMEMBER('sysadmin');

-- What databases exist?
SELECT name FROM sys.databases;

-- Switch database
USE <database>;

-- What tables exist?
SELECT name FROM sys.tables;

-- What columns does a table have?
SELECT COLUMN_NAME, DATA_TYPE
FROM information_schema.columns
WHERE TABLE_NAME='<table>';

-- Read a table
SELECT * FROM <table>;

-- List database users
SELECT name FROM sys.database_principals;

-- List server logins
SELECT name, type_desc
FROM master.sys.server_principals;

-- Check xp_cmdshell
EXEC sp_configure 'xp_cmdshell';

-- Enable xp_cmdshell
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;

-- Execute Windows command
EXEC xp_cmdshell '<command>';

-- Linked servers
EXEC sp_linkedservers;
```

### MSSQL Pentesting Command Reference

| Category | Command / Syntax | What it does |
| :--- | :--- | :--- |
| **Connection** | `sqsh -S <IP> -U <user> -P <password>` | Connects to MSSQL using `sqsh`. |
| **Connection** | `mssqlclient.py <user>@<IP> -windows-auth` | Connects using Windows/AD authentication through Impacket. |
| **Connection** | `mssqlclient.py '<domain>/<user>:<password>@<IP>'` | Connects using domain credentials. |
| **Connection** | `mssqlclient.py '<user>:<password>@<IP>'` | Connects using SQL authentication. |
| **Identity** | `SELECT SYSTEM_USER;` | Shows the current login/user identity. |
| **Identity** | `SELECT USER_NAME();` | Shows the current database user. |
| **Privileges** | `SELECT IS_SRVROLEMEMBER('sysadmin');` | Returns `1` if the current login is a `sysadmin`. |
| **Privileges** | `SELECT IS_MEMBER('db_owner');` | Returns `1` if the current user belongs to `db_owner`. |
| **Enumeration** | `SELECT @@VERSION;` | Displays MSSQL version and server information. |
| **Enumeration** | `SELECT DB_NAME();` | Shows the current database. |
| **Enumeration** | `SELECT name FROM master.dbo.sysdatabases;` | Lists databases on the MSSQL instance. |
| **Enumeration** | `SELECT name FROM sys.databases;` | Lists databases using the modern catalog view. |
| **Enumeration** | `SELECT table_name FROM information_schema.tables;` | Lists tables in the current database. |
| **Enumeration** | `SELECT TABLE_SCHEMA, TABLE_NAME FROM information_schema.tables;` | Lists table names together with their schemas. |
| **Enumeration** | `SELECT COLUMN_NAME, DATA_TYPE FROM information_schema.columns WHERE TABLE_NAME='<table>';` | Lists columns and their data types for a table. |
| **Database** | `USE <database>;` | Switches to another database. |
| **Database** | `SELECT name FROM sys.tables;` | Lists tables in the current database. |
| **Database** | `SELECT * FROM <table>;` | Displays all rows/columns from a table. |
| **Database** | `SELECT TOP 10 * FROM <table>;` | Displays the first 10 rows from a table. |
| **Database** | `SELECT * FROM <table> WHERE <column>='<value>';` | Searches a table for a specific value. |
| **Users** | `SELECT name FROM sys.database_principals;` | Lists database principals/users/roles. |
| **Users** | `SELECT name FROM master.sys.server_principals;` | Lists server-level logins and principals. |
| **Users** | `SELECT name, type_desc FROM master.sys.server_principals;` | Lists server principals with their types. |
| **Roles** | `SELECT IS_SRVROLEMEMBER('public');` | Checks membership in a server role. |
| **Configuration** | `EXEC sp_configure;` | Displays configurable server options. |
| **Configuration** | `EXEC sp_configure 'show advanced options', 1; RECONFIGURE;` | Enables viewing advanced configuration options. |
| **RCE Check** | `EXEC sp_configure 'xp_cmdshell';` | Checks the current `xp_cmdshell` configuration. |
| **RCE Enable** | `EXEC sp_configure 'xp_cmdshell', 1; RECONFIGURE;` | Enables `xp_cmdshell` when permitted. |
| **RCE Run** | `EXEC xp_cmdshell '<command>';` | Executes a Windows command through `cmd.exe`. |
| **RCE Disable** | `EXEC sp_configure 'xp_cmdshell', 0; RECONFIGURE;` | Disables `xp_cmdshell`. |
| **File Read** | `SELECT * FROM OPENROWSET(BULK '<path>', SINGLE_CLOB) AS x;` | Attempts to read a local file as text. |
| **Stored Procedures** | `SELECT name FROM sys.procedures;` | Lists stored procedures in the current database. |
| **Linked Servers** | `EXEC sp_linkedservers;` | Lists configured linked servers. |
| **Linked Servers** | `SELECT * FROM sys.servers;` | Displays server/linked-server configuration. |
| **SQL Agent** | `SELECT name, enabled FROM msdb.dbo.sysjobs;` | Lists SQL Server Agent jobs. |
| **Current DB** | `SELECT DB_NAME();` | Displays the database currently being used. |
| **Current Login** | `SELECT ORIGINAL_LOGIN();` | Shows the original login used to establish the session. |