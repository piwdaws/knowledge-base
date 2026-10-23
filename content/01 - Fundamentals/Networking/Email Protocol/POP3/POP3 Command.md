
| Command | State Allowed | Purpose / Description | Example Usage | Common Responses |
| :--- | :--- | :--- | :--- | :--- |
| **`USER`** | Authorization | Identifies the user attempting to access the mailbox. | `USER john_doe` | `+OK`, `-ERR` |
| **`PASS`** | Authorization | Submits the password for the previously specified user. | `PASS secret123` | `+OK` (Logged in), `-ERR` |
| **`STAT`** | Transaction | Requests the total number of messages and total size of the mailbox in bytes. | `STAT` | `+OK 3 15024` |
| **`LIST`** | Transaction | Lists the message numbers and their respective sizes. Can query a single message. | `LIST` or `LIST 2` | `+OK`, `-ERR` |
| **`RETR`** | Transaction | Retrieves the entire raw content of a specific message by its number. | `RETR 1` | `+OK` (followed by text), `-ERR` |
| **`DELE`** | Transaction | Marks a specific message for deletion. The server removes it when the session closes. | `DELE 1` | `+OK`, `-ERR` |
| **`NOOP`** | Transaction | Sends a dummy command to keep the session alive and prevent timeout disconnects. | `NOOP` | `+OK` |
| **`RSET`** | Transaction | Resets the session, unmarking any messages that were flagged for deletion. | `RSET` | `+OK` |
| **`TOP`** | Transaction | Retrieves the headers and a specified number of lines of the message body. | `TOP 1 10` | `+OK`, `-ERR` |
| **`UIDL`** | Transaction | Lists unique ID strings assigned to each message (helps clients track what's downloaded). | `UIDL` or `UIDL 1` | `+OK`, `-ERR` |
| **`CAPA`** | Authorization/Transaction | Requests a list of extensions and capabilities supported by the POP3 server. | `CAPA` | `+OK` (followed by capabilities) |
| **`STLS`** | Authorization | Upgrades an unencrypted plaintext POP3 session to a secure TLS/SSL session. | `STLS` | `+OK`, `-ERR` |
| **`QUIT`** | Any | Enters the Update state, commits deletions to disk, and closes the connection. | `QUIT` | `+OK` |
