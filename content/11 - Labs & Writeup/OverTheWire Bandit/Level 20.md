# ❓Question

To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

# 📋 Walkthrough

Theres a setuid binary in home directory. So they want us to execute it to see how to use it.

```bash
bandit19@bandit:~$ ls -la
total 36
drwxr-xr-x   2 root     root      4096 Jun 24 14:59 .
drwxr-xr-x 150 root     root      4096 Jun 24 15:02 ..
-rw-r--r--   1 root     root       220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root     root      3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root       807 Feb 13 12:16 .profile
-rwsr-x---   1 bandit20 bandit19 14880 Jun 24 14:59 bandit20-do
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do whoami
bandit19@bandit:~$ ./bandit20-do whoami
bandit20
```

We see it says the owner is bandit20 and its group bandit19. The '-rwsr-' means that we can execute the binary, but we execute as bandit20 instead of bandit19.

Think of it like we have a cardkey(bandit20-do) for bandit20. Means we can open the /etc/bandit_pass of bandit20. 

```bash
bandit19@bandit:~$ ls /etc/bandit_pass
bandit0   bandit12  bandit16  bandit2   bandit23  bandit27  bandit30  bandit4  bandit8
bandit1   bandit13  bandit17  bandit20  bandit24  bandit28  bandit31  bandit5  bandit9
bandit10  bandit14  bandit18  bandit21  bandit25  bandit29  bandit32  bandit6
bandit11  bandit15  bandit19  bandit22  bandit26  bandit3   bandit33  bandit7
bandit19@bandit:~$ ls /etc/bandit_pass/bandit20
/etc/bandit_pass/bandit20
## We cant open /etc/bandit_pass/bandit20 with normal means coz no permission
bandit19@bandit:~$ cat /etc/bandit_pass/bandit20
cat: /etc/bandit_pass/bandit20: Permission denied
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```
# 🧠 Explanation 

So there's a setuid binary. When we run it, it say it can run a command as another user

So we try to see who is this another user by running whoami as an argument for the binary and it say bandit20

bandit challenge have this directory for each user password. The problem is unless you the owner you cant open them

But the setuid binary allow us to run as another user. Combine that and trying to open the user pass directory solve this challenge