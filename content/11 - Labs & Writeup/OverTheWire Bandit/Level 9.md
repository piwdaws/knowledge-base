## ❓Question

The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

## 📋 Walkthrough 

If you open the data.txt its a mess. So we need to sort it and use the uniq command to find the only line that occur once

```bash
bandit8@bandit:~$ ls -la
total 56
drwxr-xr-x   2 root    root     4096 Jun 24 14:59 .
drwxr-xr-x 150 root    root     4096 Jun 24 15:02 ..
-rw-r--r--   1 root    root      220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root    root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root    root      807 Feb 13 12:16 .profile
-rw-r-----   1 bandit9 bandit8 33033 Jun 24 14:59 data.txt
bandit8@bandit:~$ sort data.txt | uniq -u
********************
```

## 🧠 Explanation

We use sort to sort the mess in alphabetical order

**uniq -u** take the sorted mess, look and compare its adjacent string and remove anything that is similar. 

The end result we got one strings that is not duplicate