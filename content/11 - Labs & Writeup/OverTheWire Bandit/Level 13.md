# ❓Question

The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.
If you need help with this level: a hint file can be found in the home directory.
Make sure to read the error messages as they are informative.

# 📋 Walkthrough 

Now if you ls -la you will see a ssh key and we need that. You can either copy paste to your machine or use scp to download the key 

```bash
bandit13@bandit:~$ ls -la
total 28
drwxr-xr-x   2 root     root     4096 Jun 24 14:59 .
drwxr-xr-x 150 root     root     4096 Jun 24 15:02 ..
-rw-r--r--   1 root     root      220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root     root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root      807 Feb 13 12:16 .profile
-rw-r-----   1 bandit14 bandit13  467 Jun 24 14:59 HINT
-rw-r-----   1 bandit14 bandit13 2602 Jun 24 14:59 sshkey.private
bandit13@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
                                                                   
┌──(kali㉿kali)-[~]
└─$ scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
```

Now if you try to connect using that sshkey you will encounter error because the key are too open. So you need to change its permission.

```bash
┌──(kali㉿kali)-[~]
└─$ chmod 700 sshkey.private 
                                                                                                          
┌──(kali㉿kali)-[~]
└─$ ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

Now you in bandit14

# 🧠 Explanation 

We use scp to copy the file into our machine. scp use ssh to copy a file from target into our machine

scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .

we specify the credentials and specify the file name we want to copy. since the file already in home directory its easier. 

then we specify where we want the file to live in. We use

. to specify our current directory