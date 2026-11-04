# ❓Question

There is a git repository at ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27.
From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

# 📋 Walkthrough

So we were told to copy the git repo. We can just do it from our machine if you want
Do not forget to put the port number

```bash
┌──(kali㉿kali)-[~]
└─$ git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo   
Cloning into 'repo'...
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-1
bandit27-git@bandit.labs.overthewire.org's password: 
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (3/3), done.
```


Open the folder and open the README. 

```bash
┌──(kali㉿kali)-[/tmp/tmp.PBB9poWwOT]
└─$ ls -la
total 0
drwx------  3 kali kali  60 Jul 14 02:15 .
drwxrwxrwt 12 root root 320 Jul 14 02:15 ..
drwxrwxr-x  3 kali kali  80 Jul 14 02:15 repo
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.PBB9poWwOT]
└─$ cd repo               
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.PBB9poWwOT/repo]
└─$ ls -la 
total 4
drwxrwxr-x 3 kali kali  80 Jul 14 02:15 .
drwx------ 3 kali kali  60 Jul 14 02:15 ..
drwxrwxr-x 7 kali kali 240 Jul 14 02:15 .git
-rw-rw-r-- 1 kali kali  68 Jul 14 02:15 README
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.PBB9poWwOT/repo]
└─$ cat README            
The password to the next level is: y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ
```