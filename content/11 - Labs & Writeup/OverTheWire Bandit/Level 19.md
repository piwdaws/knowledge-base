# ❓Question

The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

# 📋 Walkthrough

If we try to connect like usual, we will get kick out. So instead loggin in the machine, we can just execute the command directly with ssh

```bash
┌──(kali㉿kali)-[~]
└─$ ssh bandit18@bandit.labs.overthewire.org -p 2220 ls     
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit18@bandit.labs.overthewire.org's password: 

readme
```

We saw a readme file instead

```bash
┌──(kali㉿kali)-[~]
└─$ ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit18@bandit.labs.overthewire.org's password: 

KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI
```

# 🧠 Explanation 

What we doing here we saw a file for a while before we get kicked out

The good thing is we can execute a command while connecting to ssh

So we connect to ssh while trying to open the readme file

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```