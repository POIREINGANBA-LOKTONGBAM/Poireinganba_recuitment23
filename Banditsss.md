# BANDITS
---
---
---
## Level 0-1:
In this level we use the **'cat'** command to extract the password in the readme file.
#### password: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

---
---
## Level 1-2:
Here we cannont sinply use **cat** command hence we add **./** after cat: 
```
cat ./-
```
#### password: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
---
---
## Level 2-3:
here the spaces will make bash see it as seperate file names. we can use either:
```
cat "spaces in this filename"
```
or
```
cat spaces\ in\ this\ filename
```
#### password: aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
---
---
## Level 3-4:
We can easily see the hidden file using **ls -a**. Get to the directory find the file **.hidden** and **cat** the password.
#### password: 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
---
---
## Level 4-5:
Here we **cd** into **inhere** directory and search through the files for the password. **file07** contains the password.
#### password: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
---
---
## Level 5-6:
Since there is multiple folders in the **inhere** and even more in the each **maybehere0x** files we can use the following command to directly search human readable or ASCII texts.
```
file */{.,}* | grep "ASCII text"
du -b -a | grep 1033
```
**file */{.,}*** matches and dertermines all the files, and **du -b -a | grep 1033** gets the file with byte size 1033.
finaly we **cat** .file2.
#### password: P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
