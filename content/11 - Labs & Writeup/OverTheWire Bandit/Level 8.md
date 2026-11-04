# ❓Question

The password for the next level is stored in the file data.txt next to the word millionth

# 📋 Walkthrough 

This one is straightforward. We can just use grep "millionth" since grep will take the line with millionth on it

```bash
bandit7@bandit:~$ ls -la
total 4108
drwxr-xr-x   2 root    root       4096 Jun 24 14:59 .
drwxr-xr-x 150 root    root       4096 Jun 24 15:02 ..
-rw-r--r--   1 root    root        220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root    root       3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root    root        807 Feb 13 12:16 .profile
-rw-r-----   1 bandit8 bandit7 4184396 Jun 24 14:59 data.txt
bandit7@bandit:~$ cat data.txt | grep "millionth"
millionth       **********************
```

# 🧠 Explanation

If you open the file you, you will see a lot line of strings but we want the word that is next to millionth

To do that, we use grep to filter the strings.