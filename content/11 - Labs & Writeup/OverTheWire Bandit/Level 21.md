# ❓Question

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think

# 📋 Walkthrough

So lets see what the setuid binary do first

```bash
bandit20@bandit:~$ ls -la
total 36
drwxr-xr-x   2 root     root      4096 Jun 24 14:59 .
drwxr-xr-x 150 root     root      4096 Jun 24 15:02 ..
-rw-r--r--   1 root     root       220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root     root      3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root       807 Feb 13 12:16 .profile
-rwsr-x---   1 bandit21 bandit20 15604 Jun 24 14:59 suconnect
bandit20@bandit:~$ ./suconnect
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. 
If it receives the correct password from
the other side, the next password is transmitted back.
```

So we need to create a connection that listen to incoming connection and that connection send out the previous password

We can use netcat for this. -n so that no newline will appear for the echo and we add & so it will run on the background. The connection using -p(port) 12345

```bash
bandit20@bandit:~$ echo -n '4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA' | nc -l -p 12345 &
[1] 61
```

Now we execute the setuid binary with the port 12345

```bash
bandit20@bandit:~$ ./suconnect 12345
Read: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
Password matches, sending next password
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
[1]+  Done
```

# 🧠 Explanation 

So the setuid connect to any port in its argument and will give us the answer IF the port is saying the right password

The way to do this is we use nc combine with echo to to send the password to anyone who connect to it.