# ❓Question

The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

# 📋 Walkthrough 

Open the filename --spaces in this filename--

```bash
bandit2@bandit:~$ ls
--spaces in this filename--
bandit2@bandit:~$ cat "--spaces in this filename--" 
error: unexpected argument '--spaces in this filename--' found

  tip: to pass '--spaces in this filename--' as a value, use '-- --spaces in this filename--'

Usage: cat [OPTION]... [FILE]...

For more information, try '--help'.
bandit2@bandit:~$ cat ./"--spaces in this filename--"
```

# 🧠 Explanation

Same like before but because this file got spaces on them, you need to put quote on it so the terminal will take it as a single string.