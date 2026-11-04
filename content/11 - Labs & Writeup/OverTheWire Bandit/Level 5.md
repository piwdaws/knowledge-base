# ❓Question

The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.


# 📋 Walkthrough 

Change directory to inhere and you will see lot of of files. The one we looking for is the human-readable file. So we can

```bash
bandit4@bandit:~$ ls -la
total 24
drwxr-xr-x   3 root root 4096 Jun 24 14:59 .
drwxr-xr-x 150 root root 4096 Jun 24 15:02 ..
-rw-r--r--   1 root root  220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root root 3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root root  807 Feb 13 12:16 .profile
drwxr-xr-x   2 root root 4096 Jun 24 14:59 inhere
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls -la 
total 48
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file00
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file01
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file02
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file03
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file04
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file05
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file06
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file07
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file08
-rw-r----- 1 bandit5 bandit4   33 Jun 24 14:59 -file09
drwxr-xr-x 2 root    root    4096 Jun 24 14:59 .
drwxr-xr-x 3 root    root    4096 Jun 24 14:59 ..
bandit4@bandit:~/inhere$ find . -type f -exec file {} + | grep text
./-file09: Motorola S-Record; binary data in text format
./-file07: ASCII text
bandit4@bandit:~/inhere$ cat ./-file07
************************
```

# 🧠 Explanation

**find . -type f -exec file {} + | grep text**

**find .** = search for file and list all of it in the current directory and its subdirectory also

**-type f** = Only show the regular files ignore directory and etc

**-exec** = execute external command for every file **find** discover

**file** = Check the content of the file and tell what data it hold

**{} +** = Instead of checking one by one, we gather all the stuff **find** discover into a single batch and pass it into **file** 

**| grep text** = send the output of file into grep and show only line with text