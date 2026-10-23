
| Command | Purpose / Description | Example Usage | Common Responses |
| :--- | :--- | :--- | :--- |
| **`LOGIN`** | Identifies the client and provides the plaintext username and password. | `A001 LOGIN user password` | `OK` (Success), `NO` (Failed) |
| **`AUTHENTICATE`** | Initiates a secure, multi-step authentication mechanism (e.g., CRAM-MD5, OAuth). | `A002 AUTHENTICATE PLAIN` | `+` (Challenge), `OK` |
| **`SELECT`** | Opens a specific mailbox (like `INBOX`) so messages can be read or manipulated. | `A003 SELECT INBOX` | `OK [READ-WRITE]`, `NO` |
| **`EXAMINE`** | Opens a mailbox in read-only mode to prevent accidental changes to message flags. | `A004 EXAMINE INBOX` | `OK [READ-ONLY]` |
| **`CREATE`** | Creates a new mailbox or folder with the specified name. | `A005 CREATE Folders/Work` | `OK` (Success), `NO` (Exists) |
| **`DELETE`** | Permanently removes an entire mailbox or folder. | `A006 DELETE Folders/Work` | `OK`, `NO` (Permission denied) |
| **`RENAME`** | Changes the name of an existing mailbox or folder. | `A007 RENAME OldName NewName` | `OK` |
| **`SUBSCRIBE`** | Adds a folder to the server's subscription list (used by clients to filter folder views). | `A008 SUBSCRIBE INBOX/Receipts` | `OK` |
| **`UNSUBSCRIBE`** | Removes a folder from the client's subscription list. | `A009 UNSUBSCRIBE INBOX/Receipts`| `OK` |
| **`LIST`** | Retrieves a list of available mailboxes matching a specified pattern. | `A010 LIST "" "*"` | `* LIST (...)`, `OK` |
| **`LSUB`** | Retrieves a list of only the *subscribed* mailboxes. | `A011 LSUB "" "*"` | `* LSUB (...)`, `OK` |
| **`STATUS`** | Queries the state of a closed mailbox (e.g., count of total messages, unread, or recent). | `A012 STATUS INBOX (MESSAGES)` | `* STATUS INBOX ...`, `OK` |
| **`APPEND`** | Appends a raw email message directly into a specified mailbox (often used for drafts or sent items). | `A013 APPEND Drafts (\Seen) {300}` | `+` (Ready for data), `OK` |
| **`CHECK`** | Requests the server to perform a checkpoint/flush data to disk for the active mailbox. | `A014 CHECK` | `OK` |
| **`CLOSE`** | Permanently deletes all messages marked with the `\Deleted` flag and closes the active mailbox. | `A015 CLOSE` | `OK` |
| **`EXPUNGE`** | Permanently deletes all messages marked with the `\Deleted` flag without closing the mailbox. | `A016 EXPUNGE` | `* 5 EXPUNGE`, `OK` |
| **`SEARCH`** | Searches the active mailbox for messages matching specific criteria (e.g., date, sender). | `A017 SEARCH FROM "boss"` | `* SEARCH 2 5 12`, `OK` |
| **`FETCH`** | Retrieves specific data (headers, flags, body text, or attachments) of a specific message. | `A018 FETCH 12 BODY[TEXT]` | `* 12 FETCH ...`, `OK` |
| **`STORE`** | Alters flags associated with a message (e.g., marking a message as read with `\Seen` or flagged). | `A019 STORE 12 +FLAGS (\Seen)` | `* 12 FETCH ...`, `OK` |
| **`COPY`** | Copies specified messages from the current mailbox to a destination mailbox. | `A020 COPY 12 Archived` | `OK` |
| **`MOVE`** | Moves specified messages to a destination mailbox (essentially copies them and flags originals as deleted). | `A021 MOVE 12 Archived` | `OK` |
| **`CAPABILITY`** | Requests a list of features, security protocols, and extensions supported by the IMAP server. | `A022 CAPABILITY` | `* CAPABILITY ...`, `OK` |
| **`NOOP`** | Sends a dummy command to keep the session alive and poll for new server-side updates. | `A023 NOOP` | `OK` |
| **`LOGOUT`** | Terminates the active IMAP session and closes the connection. | `A024 LOGOUT` | `* BYE`, `OK` |
