# ❓Question

Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.
NOTE: if you’re a Windows user and typically use Powershell to ssh into bandit: Powershell is known to cause issues with the intended solution to this level. You should use command prompt instead.

# 📋 Walkthrough

To start with we need to see what kind of shell user bandit26 use. We can see it in /etc/passwd.

```bash
bandit25@bandit:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```

We can see that once bandit26 login. Instead the normal /bin/bash. It execute /usr/bin/showtext.

Opening the script. We can see that it execute more to a text.txt file and exit.
If you ls the home directory you will found a sshkey. 

Connecting to bandit26 with the sshkey will closed the connection.

```bash
bandit25@bandit:~$ ls
bandit26.sshkey
bandit25@bandit:~$ ssh -i bandit26.sshkey bandit26@localhost
The authenticity of host 'localhost (127.0.0.1)' can't be established.       
ED25519 key fingerprint is: SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY
This key is not known by any other names.                                    
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes     
Could not create directory '/home/bandit25/.ssh' (Permission denied).        
Failed to add the host to the list of known hosts (/home/bandit25/.ssh/known_hosts).
                                                                             
                      This is an OverTheWire game server.                    
            More information on http://www.overthewire.org/wargames          
                                                                             
!!! You are trying to log into this SSH server on port 22, which is not intended.
!!! If you are trying to log in to an OverTheWire game, use the port mentioned in
!!! the "SSH Information" on that game's webpage (in the top left corner).   
                                                                             
bandit26@localhost: Permission denied (publickey).                           
bandit25@bandit:~$     
```

The reason because once we login to bandit26. It execute more text.txt.

More is a command line that used to view the contents of a text file one screenful at a time.

The things with more. If your terminal is large enough more will think everything is fit and nothing to paginate. So it exit immediately.

The workaround for this would be change the terminal abit smaller to overload the buffer and try login again.

What work with me is i shrink the terminal and spam v till these appear


```bash
 _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
-- VISUAL --   
```

Why v? V to enter vim a text editor. After that we use :e /etc/bandit_pass/bandit26

Why :e ? : in vim is like entering command mode and e is edit. so its like we telling vim to edit /etc/bandit_pass/bandit26

Since this vim is running as bandit26 we can open the file.

```bash
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
:e /etc/bandit_pass/bandit26
```

```bash
jHdv2ELQhT22BkprMNDjybZDAkw1zeBJ
~                                                                                                         
~                                                                                                    
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
~                                                                                                         
"/etc/bandit_pass/bandit26" [readonly] 1L, 33B           
```

Do not close the terminal yet coz we still need it