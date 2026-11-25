- Generates ~200 likely username permutations per name, takes a name list, a URL, or a file as input
- Faster than manually writing out firstname/lastname/initials combos by hand

```bash
namebuster "John Broccoli, Diana Mango"     # from names directly
namebuster https://sauna.htb                # scrapes the site itself for names first
namebuster document.txt                     # pulls names out of a file
```

- Output is a plain username list, feed it straight into [[05 - Credential Hunting]]'s username-confirming step:
```bash
namebuster https://company.com > usernames.txt
kerbrute userenum usernames.txt -d DOMAIN.LOCAL --dc dc.company.com
```
- Basically does the job you'd otherwise do manually in [[06 - Attacking Active Directory and NTDS]] (guessing naming conventions by hand), just automated