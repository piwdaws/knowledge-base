# ❓Question

The password for the next level is stored somewhere on the server and has all of the following properties:
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

# 📋 Walkthrough 

It say and highlight it was somewhere on the server. Instead using find . we need to use find / which translate to look at all the directory starting the root directory

```bash
bandit6@bandit:~$ find . -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
**********************
```

# 🧠 Explanation

Now the problem is, somewhere on the server. So we need to scourge the directory and its subdirectory and all those dir and file. So we automate it

**find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null**

**/** is used to start looking from the root directory

**2>/dev/null** is used to throw all the error away into the null