## ❓Question

The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

## 📋 Walkthrough 

Now we need to use combination of strings and grep command

```bash
bandit9@bandit:~$ ls -la
total 40
drwxr-xr-x   2 root     root     4096 Jun 24 14:58 .
drwxr-xr-x 150 root     root     4096 Jun 24 15:02 ..
-rw-r--r--   1 root     root      220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root     root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root      807 Feb 13 12:16 .profile
-rw-r-----   1 bandit10 bandit9 19382 Jun 24 14:58 data.txt
bandit9@bandit:~$ strings data.txt | grep ==
cL0========== the
========== password
>========== is
R========== B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

## 🧠 Explanation

We use strings to show only strings that is text not those weird text and we pipe it into

grep == to filter the result. since they said it was preceded by several =