# ❓Question

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

#📋 Walkthrough 

Now we need to submit the current password using SSL/TLS. For this we can use opessl to connect to the localhost. Then submit the current password

```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001
Connecting to 127.0.0.1
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
------
read R BLOCK
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
Correct!
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

# 🧠 Explanation 

From my understanding ssl/tls is how HTTPS encrypted our traffic making it secure

Instead or normally connect with nc, we use openssl to connect with the localhost. Pass the password and done