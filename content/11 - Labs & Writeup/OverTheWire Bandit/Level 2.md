# ❓Question

The password for the next level is stored in a file called - located in the home directory

# 📋 Walkthrough 

Open the file named - 
Since its a dashed filename we need to open it using its relative path 

```bash
bandit1@bandit:~$ cat -
^C
bandit1@bandit:~$ cat /-
cat: /-: No such file or directory
bandit1@bandit:~$ cat ./-
****************************
```

# 🧠 Explanation

We cant open it normally because the terminal or the command line parser confused the file name with flag or command flag

normally command flag use - on it

Example:
nmap -sC -sV 192.168.0.1

So we need to open the file through its relative path instead. 
. means look at our current directory
/ means open the file or look inside it