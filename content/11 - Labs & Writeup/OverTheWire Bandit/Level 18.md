# ❓Question

There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

# 📋 Walkthrough

For start. Connect to bandit17 using the sshkey from previous question. I named my sshkey as bandit17. Make sure to change its permission

```bash
┌──(kali㉿kali)-[~]
└─$ nano bandit17 
                                                                                                          
┌──(kali㉿kali)-[~]
└─$ chmod 700 bandit17                
                                                                                                          
┌──(kali㉿kali)-[~]
└─$ ssh -i bandit17 bandit17@bandit.labs.overthewire.org -p 2220
```

So we need to compare both file and see which line is changed between them. Connect to bandit18 and if it say Byebye! its the right one

We use the command diff to compare it. diff <old file> <new file>

```bash
bandit17@bandit:~$ ls -la
total 36
drwxr-xr-x   3 root     root     4096 Jun 24 14:59 .
drwxr-xr-x 150 root     root     4096 Jun 24 15:02 ..
-rw-r-----   1 bandit17 bandit17   33 Jun 24 14:59 .bandit16.password
-rw-r--r--   1 root     root      220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root     root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root      807 Feb 13 12:16 .profile
drwxr-xr-x   2 root     root     4096 Jun 24 14:59 .ssh
-rw-r-----   1 bandit18 bandit17 3300 Jun 24 14:59 passwords.new
-rw-r-----   1 bandit18 bandit17 3300 Jun 24 14:59 passwords.old
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< icUh23IUytZLIYhcCaXL18agiSIqymBc
---
> OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

Connect to bandit18 and see if its working