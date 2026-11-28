## Concept of Attacks (a mental checklist for breaking down ANY vuln)
- Every attack/vuln can be broken into 4 parts, useful when reading about a new CVE or debugging why something worked
- **Source** - where the bad input/data comes from (code, config, API, user input)
- **Process** - what actually processes that input, and the bug in how it processes it
- **Privileges** - what permission level the process runs at (this is WHY the bug matters, a bug running as root/SYSTEM is way worse than one running as a low-priv user)
- **Destination** - where the result goes (local file/service, or out over the network to the attacker)

- Example: Log4j (CVE-2021-44228) - attacker puts a JNDI lookup in the HTTP User-Agent header (**Source**) → the logging library misreads it as a command instead of plain text (**Process**) → runs with the app's often-admin-level logging permissions (**Privileges**) → fetches and runs attacker's malicious code from a remote server (**Destination**) = RCE

## Common Service Misconfigurations (checklist to check on every service)
- **Default/weak creds** - still check for these even on "modern" setups: `admin:admin`, `admin:password`, blank password
- **Anonymous auth allowed** - some services let anyone connect with no login at all (classic on FTP)
- **Misconfigured access rights** - a low-priv account that can read way more than it should (e.g. an upload-only FTP user who can actually read every file)
- **Unnecessary defaults left on** - default pages/ports/accounts/features never disabled after setup, debugging/admin interfaces left exposed, error messages leaking stack traces

## Finding Sensitive Information (mindset)
- Treat every small finding as a lead, not a dead end — a single leaked username in an empty FTP file can chain into a password in an email into DB access into RCE
- Before digging in: understand what the target actually does (their business/purpose) so you know what kind of sensitive info is even worth looking for
- What counts as "sensitive": usernames, emails, passwords, DNS records, IPs, source code, config files, PII
- This same mindset applies to [[05 - Credential Hunting]] work already covered — don't just grep for "password", follow every small clue