## Open Relay 
```bash 
# Wespecify the port as port 25
# We use the NSE Script with an attemp to send email

sudo nmap 10.129.14.128 -p25 --script smtp-open-relay -v
```