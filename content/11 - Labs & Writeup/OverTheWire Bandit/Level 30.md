# ❓Question

There is a git repository at ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo via the port 2220. The password for the user bandit29-git is the same as for the user bandit29.
From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

# 📋 Walkthrough

We start the same like before

```bash
┌──(kali㉿kali)-[/tmp/tmp.oldjYfSdUx]
└─$ git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo 
Cloning into 'repo'...
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit29-git@bandit.labs.overthewire.org's password: 

remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 16 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (2/2), done.
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.oldjYfSdUx]
└─$ 
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.oldjYfSdUx]
└─$ ls -la
total 0
drwx------  3 kali kali  60 Jul 15 02:25 .
drwxrwxrwt 14 root root 360 Jul 15 02:24 ..
drwxrwxr-x  3 kali kali  80 Jul 15 02:25 repo
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.oldjYfSdUx]
└─$ cd repo               
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.oldjYfSdUx/repo]
└─$ ls -la
total 4
drwxrwxr-x 3 kali kali  80 Jul 15 02:25 .
drwx------ 3 kali kali  60 Jul 15 02:25 ..
drwxrwxr-x 7 kali kali 240 Jul 15 02:25 .git
-rw-rw-r-- 1 kali kali 131 Jul 15 02:25 README.md
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.oldjYfSdUx/repo]
└─$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```

So might be about git branch since it say no passwords in production. Most likely theres a branch for development. For this we can use git branch -a to see all the branch

```bash
┌──(kali㉿kali)-[/tmp/tmp.oldjYfSdUx/repo]
└─$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
```

From here we need to switch branch. Since passowrd not in production. It might be in development. So try switch there

```bash
┌──(kali㉿kali)-[/tmp/tmp.oldjYfSdUx/repo]
└─$ git switch dev                                   
branch 'dev' set up to track 'origin/dev'.
Switched to a new branch 'dev'
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.oldjYfSdUx/repo]
└─$ ls -la
total 4
drwxrwxr-x 4 kali kali 100 Jul 15 02:28 .
drwx------ 3 kali kali  60 Jul 15 02:25 ..
drwxrwxr-x 2 kali kali  60 Jul 15 02:28 code
drwxrwxr-x 7 kali kali 240 Jul 15 02:28 .git
-rw-rw-r-- 1 kali kali 134 Jul 15 02:28 README.md
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.oldjYfSdUx/repo]
└─$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX
```