# ❓Question

After all this git stuff, it’s time for another escape. Good luck!

# 📋 Walkthrough

Once we login we saw that everytime we try to use a command it just turn it into uppercase

```bash
WELCOME TO THE UPPERCASE SHELL
>> 
>> :e shell
sh: 1: :E: Permission denied
>> whoami
sh: 1: WHOAMI: Permission denied
>> 
```

So in bash every variable begin $

Specifically theres a variable $0 which if you tried to echo it. it will return the current shell or script

```bash
┌──(kali㉿kali)-[~]
└─$ echo $0                        
/usr/bin/zsh
```

So if we use $0 it will try to change it into uppercase but since it cant the bash expand the the variables which is the current shell then bash run effectively

```bash
>> $0
$ ls -la
total 36
drwxr-xr-x   2 root     root      4096 Jun 24 14:59 .
drwxr-xr-x 150 root     root      4096 Jun 24 15:02 ..
-rw-r--r--   1 root     root       220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root     root      3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root       807 Feb 13 12:16 .profile
-rwsr-x---   1 bandit33 bandit32 15136 Jun 24 14:59 uppershell
```

We saw that the uppershell is run as bandit33 so we use whoami to see what user we are and it was bandit33. From here we can open the file to see what bandit33 password is

```bash
$ whoami
bandit33
$ cat /etc/bandit_pass/bandit33
u4P2CyPOwPGLe94RdD9Uo2FxFwvnFswM
```