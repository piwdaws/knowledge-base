- Packet analyzer, can read live traffic or opened pcap files, has a strong filter engine

---
ip.addr == 10.10.10.1  
tcp.port == 80  
http  
dns  
http.request.method == "POST"  
tcp.flags.syn == 1 && tcp.flags.ack == 0 # SYN packets, scan/connection attempts  
tcp.stream eq 53 # follow one specific conversation

- For creds specifically: filter `http`, look for POST requests, open them and check form data
- Or just search directly: `http contains "passw"` / Edit > Find Packet