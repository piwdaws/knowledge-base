## Some Important Command
```sql
-- Who am I? 
SELECT USER(); 
SELECT CURRENT_USER(); 

-- What version? 
SELECT VERSION(); 

-- What is the server hostname? 
SELECT @@hostname; 

-- What databases can I access? 
SHOW DATABASES; 

-- What database am I currently using? 
SELECT DATABASE(); 

-- Switch database 
USE <database>; 

-- What tables exist? 
SHOW TABLES; 

-- What columns does a table have? 
SHOW COLUMNS FROM <table>; 

-- Alternative table structure command 
DESCRIBE <table>; 

-- Read a table 
SELECT * FROM <table>; 

-- Read the first 10 rows 
SELECT * FROM <table> LIMIT 10; 

-- Search for a specific value 
SELECT * FROM <table> WHERE <column>='<value>'; 

-- List MySQL users 
SELECT user, host FROM mysql.user; 

-- Check current privileges 
SHOW GRANTS; 

-- Check another user's privileges 
SHOW GRANTS FOR '<user>'@'<host>'; 

-- Check secure_file_priv 
SHOW VARIABLES LIKE 'secure_file_priv'; 

-- Find MySQL data directory 
SELECT @@datadir; 

-- Read a file 
SELECT LOAD_FILE('<path>'); 

-- Write query output to a file 
SELECT '<data>' INTO OUTFILE '<path>'; 

-- Write raw data to a file 
SELECT '<data>' INTO DUMPFILE '<path>';

```

### MySQL Pentesting Command Reference

| Category | Command / Syntax | What it does |
| :--- | :--- | :--- |
| **Connection** | `mysql -u <user> -p<password> -h <IP>` | Connects to a MySQL server using username, password, and target IP. |
| **Connection** | `mysql -u <user> -p -h <IP>` | Connects and prompts for the password interactively. |
| **Connection** | `mysql -u <user> -h <IP>` | Attempts to connect without providing a password. |
| **Enumeration** | `SELECT VERSION();` | Displays the MySQL/MariaDB server version. |
| **Enumeration** | `SHOW DATABASES;` | Lists all databases accessible to the current user. |
| **Enumeration** | `SELECT DATABASE();` | Shows the currently selected database. |
| **Enumeration** | `SHOW STATUS;` | Displays server status information. |
| **Enumeration** | `SHOW VARIABLES;` | Displays MySQL server configuration variables. |
| **Database** | `USE <database>;` | Selects a database to work with. |
| **Database** | `SHOW TABLES;` | Lists tables in the currently selected database. |
| **Database** | `SHOW COLUMNS FROM <table>;` | Displays the columns and their definitions for a table. |
| **Database** | `DESCRIBE <table>;` | Displays the structure of a table. |
| **Database** | `SELECT * FROM <table>;` | Displays all rows and columns from a table. |
| **Database** | `SELECT * FROM <table> LIMIT 10;` | Displays the first 10 rows from a table. |
| **Database** | `SELECT * FROM <table> WHERE <column>='<value>';` | Searches a table for a specific value. |
| **Users** | `SELECT user, host FROM mysql.user;` | Lists MySQL users and the hosts they can connect from. |
| **Users** | `SELECT user, host, authentication_string FROM mysql.user;` | Displays MySQL users and stored authentication data. |
| **Privileges** | `SHOW GRANTS FOR '<user>'@'<host>';` | Displays the privileges assigned to a MySQL account. |
| **Privileges** | `SHOW GRANTS;` | Displays privileges for the current account. |
| **Configuration** | `SHOW VARIABLES;` | Displays MySQL configuration variables. |
| **Configuration** | `SHOW VARIABLES LIKE '%secure%';` | Searches configuration variables related to security/file access. |
| **Configuration** | `SHOW VARIABLES LIKE 'secure_file_priv';` | Checks the `secure_file_priv` restriction. |
| **File Read** | `SELECT LOAD_FILE('<path>');` | Attempts to read a file from the MySQL server filesystem. |
| **File Write** | `SELECT '<data>' INTO OUTFILE '<path>';` | Writes query output to a file on the server filesystem when permitted. |
| **File Write** | `SELECT '<data>' INTO DUMPFILE '<path>';` | Writes raw data to a file on the server filesystem when permitted. |
| **Database Files** | `SELECT @@datadir;` | Shows the directory where MySQL stores database files. |
| **Privileges** | `SELECT USER();` | Shows the MySQL account and client host used for authentication. |
| **Privileges** | `SELECT CURRENT_USER();` | Shows the account MySQL used to authenticate the connection. |
| **System Info** | `SELECT @@hostname;` | Displays the MySQL server hostname. |
| **System Info** | `SELECT @@version_compile_os;` | Displays the operating system MySQL was compiled for. |
| **System Info** | `SELECT @@version_compile_machine;` | Displays the architecture MySQL was compiled for. |
| **Exit** | `EXIT;` | Closes the MySQL client session. |
| **Exit** | `QUIT;` | Closes the MySQL client session. |
