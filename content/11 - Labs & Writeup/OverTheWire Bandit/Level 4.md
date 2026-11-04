# ❓Question

The password for the next level is stored in a hidden file in the inhere directory.


# 📋 Walkthrough 

The directory is hidden so you need to

```bash
bandit3@bandit:~$ ls -la
total 24
drwxr-xr-x   3 root root 4096 Jun 24 14:59 .
drwxr-xr-x 150 root root 4096 Jun 24 15:02 ..
-rw-r--r--   1 root root  220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root root 3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root root  807 Feb 13 12:16 .profile
drwxr-xr-x   2 root root 4096 Jun 24 14:59 inhere
bandit3@bandit:~$ cat inhere
cat: inhere: Is a directory
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 Jun 24 14:59 .
drwxr-xr-x 3 root    root    4096 Jun 24 14:59 ..
-rw-r----- 1 bandit4 bandit3   33 Jun 24 14:59 ...Hiding-From-You
bandit3@bandit:~/inhere$ cat "...Hiding-From-You" 
**********************
```

# 🧠 Explanation

The directory is hidden. If you use the normal **ls** you wont see it

So you need to use **-la** options.

**-la** basically say show the detailed of the files and show all of the hidden stuff you hide from us