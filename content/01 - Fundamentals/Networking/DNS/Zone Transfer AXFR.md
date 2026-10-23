## Zone Transfer
To prevent company website to go offline if one server crashes, people do this Master and Slave.

The Primary ( Master ): The main server where the IT Administrator perform changes
The Secondary( Slaves ): Backup Server. Doesnt create anything just copy from master

---
### How they stay Synchronised 
- To keep them identical, the slave look at master every hours
- Its check the serial number in the SOA Record.
- If master serial number changes, the slave will copy 

---
### Zone Transfer AXFR 
- If slave noticed the number different, it will ask master to send over entire updated list network over TCP port 53. This is called Zone Transfer.
- To prevent stranger from copy it, server used a safe password (rndc-key)

---
## Zone Transfer Diagram
![[Screenshot 2026-09-17 at 2.45.25 PM.png]]