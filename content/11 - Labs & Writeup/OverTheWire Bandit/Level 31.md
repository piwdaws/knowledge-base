# ❓Question

There is a git repository at ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo via the port 2220. The password for the user bandit30-git is the same as for the user bandit30.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

# 📋 Walkthrough

We do the same like before

```bash
┌──(kali㉿kali)-[/tmp/tmp.a2u1OvBiWn]
└─$ git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
Cloning into 'repo'...
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit30-git@bandit.labs.overthewire.org's password: 

remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (4/4), done.
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.a2u1OvBiWn]
└─$ 
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.a2u1OvBiWn]
└─$ ls -la                
total 0
drwx------  3 kali kali  60 Jul 15 02:33 .
drwxrwxrwt 15 root root 380 Jul 15 02:33 ..
drwxrwxr-x  3 kali kali  80 Jul 15 02:33 repo
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.a2u1OvBiWn]
└─$ cd repo               
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.a2u1OvBiWn/repo]
└─$ ls -la
total 4
drwxrwxr-x 3 kali kali  80 Jul 15 02:33 .
drwx------ 3 kali kali  60 Jul 15 02:33 ..
drwxrwxr-x 7 kali kali 240 Jul 15 02:33 .git
-rw-rw-r-- 1 kali kali  30 Jul 15 02:33 README.md
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.a2u1OvBiWn/repo]
└─$ cat README.md
just an epmty file... muahaha
```

We got this empty file instead. We can look at its tag. 

```bash
┌──(kali㉿kali)-[/tmp/tmp.a2u1OvBiWn/repo]
└─$ git tag                                                                             
secret
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.a2u1OvBiWn/repo]
└─$ git show secret                                  
82NkymblpGBYmIXG6ZQ8YldBYstHpfUf
```

# 🧠 Explanation

git tag is a named label that points to a specific commit.
Unlike commit. It doesnt move
Usually it used to mark important point like bookmark. 
And we can see it with git show [tag]