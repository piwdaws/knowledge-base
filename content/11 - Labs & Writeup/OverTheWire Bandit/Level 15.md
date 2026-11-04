# ❓Question

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

# 📋 Walkthrough 

Previous question stated that the bandit14 password is stored in /etc/bandit_pass/bandit14

So lets get that first

```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

Then it want us to submit to localhost port 30000. So we nc to the localhost 30000 

And send the password there

```bash
bandit14@bandit:~$ nc localhost 30000
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
Correct!
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

# 🧠 Explanation 

We use nc to connect to localhost and specify the port 30000