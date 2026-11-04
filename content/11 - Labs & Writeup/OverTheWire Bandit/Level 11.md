# ❓Question

The password for the next level is stored in the file data.txt, which contains base64 encoded data

# 📋 Walkthrough 

We need to decode the content of data.txt with base64 so we can do like this

```bash
bandit10@bandit:~$ ls -la
total 24
drwxr-xr-x   2 root     root     4096 Jun 24 14:58 .
drwxr-xr-x 150 root     root     4096 Jun 24 15:02 ..
-rw-r--r--   1 root     root      220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root     root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root      807 Feb 13 12:16 .profile
-rw-r-----   1 bandit11 bandit10   69 Jun 24 14:58 data.txt
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIHBZZk9ZNkh3VXNEajVyTDlVdnloVTdNQ212OHZONVJvCg==
bandit10@bandit:~$ echo data.txt | base64 -d
base64: error: invalid input
bandit10@bandit:~$ cat data.txt | base64 -d
The password is pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

# 🧠 Explanation 

The flag is encoded into base64. The easy way for this would be to decode it by piping it to base64 -d

-d as for decode