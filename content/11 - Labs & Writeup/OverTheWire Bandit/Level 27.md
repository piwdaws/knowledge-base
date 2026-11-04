# ❓Question

Good job getting a shell! Now hurry and grab the password for bandit27!

# 📋 Walkthrough

Make sure you still in the vim mode from previous question.
From there we will change into shell instead of vim text editor

```bash
### First we need to set our shell first
:set shell=/bin/bash
### Then we open the shell
:shell
bandit26@bandit:~$ 
```

From there we use ls to see what we got and we got bandit27-do which run a command as another user. In these case run as bandit27 maybe. and a text.txt. The reason we need to open vim text editor.

```bash
bandit26@bandit:~$ ls 
bandit27-do  text.txt
bandit26@bandit:~$ cat text.txt
  _                     _ _ _   ___   __  
 | |                   | (_) | |__ \ / /  
 | |__   __ _ _ __   __| |_| |_   ) / /_  
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \ 
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/ 
bandit26@bandit:~$ ./bandit27-do
Run a command as another user.
  Example: ./bandit27-do id
```

If we can run command as another user. So we can open the password for that user

```bash
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
STJLJBRRphMxKB392CT4iOr5CbzPU9ER
```
