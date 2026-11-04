# ❓Question

There is a git repository at ssh://bandit31-git@bandit.labs.overthewire.org/home/bandit31-git/repo via the port 2220. The password for the user bandit31-git is the same as for the user bandit31.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.



# 📋 Walkthrough

We do the same like before

```bash
┌──(kali㉿kali)-[/tmp/tmp.U6cjQQoEBh]
└─$ git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo
Cloning into 'repo'...
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit31-git@bandit.labs.overthewire.org's password: 

remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (4/4), 382 bytes | 95.00 KiB/s, done.
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.U6cjQQoEBh]
└─$ 
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.U6cjQQoEBh]
└─$ cd repo               
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.U6cjQQoEBh/repo]
└─$ cat README.md
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```

So it say we need to push a file to remote repository with the following details. So we create that file first

```bash
┌──(kali㉿kali)-[/tmp/tmp.U6cjQQoEBh/repo]
└─$ nano key.txt        
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.U6cjQQoEBh/repo]
└─$ cat key.txt  
May I come in?
```

Now we add it before commit push our file

```bash
┌──(kali㉿kali)-[/tmp/tmp.U6cjQQoEBh/repo]
└─$ git add key.txt
The following paths are ignored by one of your .gitignore files:
key.txt
hint: Use -f if you really want to add them.
hint: Disable this message with "git config set advice.addIgnoredFile false"
```

It say we need to use -f and our file is ignored coz .gitignore file. So lets delete that file first

```bash
┌──(kali㉿kali)-[/tmp/tmp.U6cjQQoEBh/repo]
└─$ cat .gitignore     
*.txt
```

Since im using my local machine. i need to set a name and email for the git 

```bash
┌──(kali㉿kali)-[/tmp/tmp.KeMLjxWxrB/repo]
└─$ git commit -a                                                                       
Author identity unknown

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'kali@kali.(none)')
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.KeMLjxWxrB/repo]
└─$ git config user.name "bandit31"
git config user.email "bandit31@overthewire.org"
```

After set it i can just commit it and give a comment with git add -m   

After that push it to the remote repository with git push -u origin master

origin as it the name of the repo and master as the name for the branch

```bash
┌──(kali㉿kali)-[/tmp/tmp.KeMLjxWxrB/repo]
└─$ git commit -m "push"
[master d94e639] push
 1 file changed, 1 insertion(+)
 create mode 100644 key.txt
                                                                                   
┌──(kali㉿kali)-[/tmp/tmp.KeMLjxWxrB/repo]
└─$ git push -u origin master      
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-1
bandit31-git@bandit.labs.overthewire.org's password: 
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 3 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (5/5), 543 bytes | 543.00 KiB/s, done.
Total 5 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote: ### Attempting to validate files... ####
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
remote: Well done! Here is the password for the next level:
remote: pWuj5jBQ6IgV0NXwiH6g1pXRF8S1YvbT 
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
To ssh://bandit.labs.overthewire.org:2220/home/bandit31-git/repo
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'ssh://bandit.labs.overthewire.org:2220/home/bandit31-git/repo'
```