## Object Identifier (OID)
- Unique address made of numbers separated by dots (like IP address). It points to a **single, specific piece of data** inside a device.
- Example : 1.3.6.5.3.3.4.0
- Function: If you ask router what data at this exact address. They will response with Device Name. Like Printer01 

## Management Information Base (MIB)
- Text file that acts as a translator. The MIB translates those ugly numbers into human-readable text.
- Think of its like DNS 
- Without it: 1.3.6.1.2.1.1.5.0 = "Router1"
- With MIB: `sysName = "Router1"`

---