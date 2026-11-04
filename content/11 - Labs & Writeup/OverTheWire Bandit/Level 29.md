# ❓Question

There is a git repository at ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo via the port 2220. The password for the user bandit28-git is the same as for the user bandit28.
From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

# 📋 Walkthrough

We will be doing the same like before. We clone the repo. Dont forget the port number

```bash
┌──(kali㉿kali)-[/tmp/tmp.01CHOmwKOa]
└─$ git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
Cloning into 'repo'...
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit28-git@bandit.labs.overthewire.org's password: 
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 9 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (9/9), done.
Resolving deltas: 100% (2/2), done.
```

Now we open the directory and open the README

```bash
┌──(kali㉿kali)-[/tmp/tmp.01CHOmwKOa]
└─$ ls -la
total 0
drwx------  3 kali kali  60 Jul 15 02:16 .
drwxrwxrwt 13 root root 340 Jul 15 02:15 ..
drwxrwxr-x  3 kali kali  80 Jul 15 02:16 repo
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.01CHOmwKOa]
└─$ cd repo               
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.01CHOmwKOa/repo]
└─$ ls -la
total 4
drwxrwxr-x 3 kali kali  80 Jul 15 02:16 .
drwx------ 3 kali kali  60 Jul 15 02:16 ..
drwxrwxr-x 7 kali kali 240 Jul 15 02:16 .git
-rw-rw-r-- 1 kali kali 111 Jul 15 02:16 README.md
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.01CHOmwKOa/repo]
└─$ cat README.md 
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```

So we got nothing. But we can try to see its commit history with git log 

```bash
┌──(kali㉿kali)-[/tmp/tmp.01CHOmwKOa/repo]
└─$ git log                                                                             
commit e2e1de5396037bafb23e9bb37c12ebea9b911cfd (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:20 2026 +0000

    fix info leak

commit 2678cfadd8f2a347bc23e1ea491f702e5b184709
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:20 2026 +0000

    add missing data

commit 9530d526c22b9e6e6ae11070ef8ff8ee21eb2e02
Author: Ben Dover <noone@overthewire.org>
Date:   Wed Jun 24 14:59:20 2026 +0000

    initial commit of README.md
```

We saw theres 3 changes happen. To see what happen on that commit we can use git show [commit hash]

```bash
┌──(kali㉿kali)-[/tmp/tmp.01CHOmwKOa/repo]
└─$ git show 9530d526c22b9e6e6ae11070ef8ff8ee21eb2e02
commit 9530d526c22b9e6e6ae11070ef8ff8ee21eb2e02
Author: Ben Dover <noone@overthewire.org>
Date:   Wed Jun 24 14:59:20 2026 +0000

    initial commit of README.md

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..7ba2d2f
--- /dev/null
+++ b/README.md
@@ -0,0 +1,8 @@
+# Bandit Notes
+Some notes for level29 of bandit.
+
+## credentials
+
+- username: bandit29
+- password: <TBD>
+
                                                                                            
┌──(kali㉿kali)-[/tmp/tmp.01CHOmwKOa/repo]
└─$ git show 2678cfadd8f2a347bc23e1ea491f702e5b184709
commit 2678cfadd8f2a347bc23e1ea491f702e5b184709
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:20 2026 +0000

    add missing data

diff --git a/README.md b/README.md
index 7ba2d2f..42331d9 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 
 - username: bandit29
-- password: <TBD>
+- password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```