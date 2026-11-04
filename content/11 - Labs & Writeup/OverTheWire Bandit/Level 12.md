# ❓Question

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

# 📋 Walkthrough 

The password was in cipher which have been rotate with 13 positions. Means if its a the cipher become n

```bash
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf TEBbmJCB8DlA0zTewHxVQ0JPLxMvDkeA
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

# 🧠 Explanation 

This is a ceaser cypher. Every letter has been rotate like 13. Easy way you can use online decoder. The other way you can

Use tr. Which i think stand for transform. Coz its swap the letter 

The syntax is 

tr 'FROM' 'TO'

So i use

tr 'A-Za-z' 'N-ZA-Mn-za-m'

The first one will list letter from A till z

ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz

The second will list letter from N till m

NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm

then tr will take the FROM letter and see which letter correspondence with the TO letter and transform to it.