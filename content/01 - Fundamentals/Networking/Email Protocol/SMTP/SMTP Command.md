
| Command         | Full Name      | Purpose / Description                                                                                | Common Response Codes                       |
| :-------------- | :------------- | :--------------------------------------------------------------------------------------------------- | :------------------------------------------ |
| **`HELO`**      | Hello          | Identifies the client to the server using the client's domain name (used in standard SMTP).          | `250` (OK)                                  |
| **`EHLO`**      | Extended Hello | Identifies the client to the server and requests service extensions (used in ESMTP).                 | `250` (OK)                                  |
| **`MAIL FROM`** | Mail From      | Initiates a mail transfer and specifies the sender's return email address.                           | `250` (OK), `550` (Access denied)           |
| **`RCPT TO`**   | Recipient To   | Identifies the recipient of the email. Can be repeated for multiple recipients.                      | `250` (OK), `550` (User unknown)            |
| **`DATA`**      | Data           | Tells the server that the message body text follows. Ended by a line containing only a period (`.`). | `354` (Start input), `250` (OK)             |
| **`RSET`**      | Reset          | Aborts the current mail transaction and clears all stored sender and recipient buffers.              | `250` (OK)                                  |
| **`VRFY`**      | Verify         | Confirms whether a specific username or mailbox exists on the server.                                | `250` (User valid), `550` (Not found)       |
| **`EXPN`**      | Expand         | Expands a mailing list to show the individual constituent email addresses.                           | `250` (OK), `550` (Access denied)           |
| **`HELP`**      | Help           | Requests a list of commands supported by the specific SMTP server.                                   | `211` (System status), `214` (Help message) |
| **`NOOP`**      | No Operation   | Forces the server to reply with an OK status code to keep the connection alive.                      | `250` (OK)                                  |
| **`QUIT`**      | Quit           | Closes the transmission channel and terminates the active SMTP session.                              | `221` (Service closing channel)             |
| **`STARTTLS`**  | Start TLS      | Upgrades an unencrypted plaintext connection to a secure TLS/SSL connection.                         | `220` (Ready to start TLS)                  |
| **`AUTH`**      | Authentication | Authenticates the client to the server using mechanisms like `LOGIN`, `PLAIN`, or `CRAM-MD5`.        | `235` (Auth successful), `334` (Challenge)  |
