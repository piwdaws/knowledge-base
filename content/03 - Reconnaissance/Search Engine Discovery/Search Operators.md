## Common Operator

| Operator | Purpose | Example |
| :--- | :--- | :--- |
| `site:` | Restrict results to a domain | `site:example.com` |
| `inurl:` | Search for a term in the URL | `inurl:login` |
| `filetype:` | Search for a specific file type | `filetype:pdf` |
| `intitle:` | Search for a term in the page title | `intitle:"confidential report"` |
| `intext:` | Search for a term in page text | `intext:"password reset"` |
| `allintext:` | Require multiple terms in page text | `allintext:admin password` |
| `allinurl:` | Require multiple terms in the URL | `allinurl:admin panel` |
| `allintitle:` | Require multiple terms in the title | `allintitle:confidential report` |
| `" "` | Search for an exact phrase | `"information security policy"` |
| `-` | Exclude a term | `site:example.com -login` |
| `OR` | Match either term | `linux OR ubuntu` |
| `*` | Wildcard | `user* manual` |
| `..` | Numerical range | `"price" 100..500` |

---
