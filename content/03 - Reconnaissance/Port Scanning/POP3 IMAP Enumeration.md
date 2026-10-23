## Footprinting service
```bash
sudo nmap 10.129.14.128 -sV -p110,143,993,995 -sC
```

---
## Using cURL to connect IMAP
```bash
# We use curl to connect
# -k to tell curl that we allow insecure connection
# imaps:// we specifies the protocol
# --user we provide the credential
# We can use -v as verbose to see the connection
# From there we might able to see the version they use and maybe the SSL cert
curl -k 'imaps://10.129.14.128' --user user:p4ssw0rd
```

---
## Using openSSL to interact server over SSL
```bash
openssl s_client -connect 10.129.14.128:pop3s
openssl s_client -connect 10.129.14.128:imaps
```

