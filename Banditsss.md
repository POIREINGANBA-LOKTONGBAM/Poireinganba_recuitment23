# !::BANDITS::!
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
---
---
## Level 6-7:
here we need to use the **find** command to get the folder with owner: bandit7, group: bandit6 and size: 33 bytes.
```
find / -type f -user bandit7 -group bandit6 -size 33c
```
I went through all the output to find the file location... luckily the destination was on the 8^th line... but we can use **2>/dev/null** to filter the permission error ones.
#### pasword: z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
---
---
## Level 7-8:
In this level we can use the **grep** command to easily display the line with the text "millionth" in it.
```
grep "millionth" data.txt
```
#### password: TESKZC0XvTetK0S9xNwm25STk5iWrBvP
---
---
## Level 8-9:
In this level we cannot use **uniq** alone. We need to first **sort** the data.txt and then use **uniq -u**.
```
sort data.txt | uniq -u
```
#### password: EN632PlfYiZbn3PhVK3XOGSlNInNE00t
---
---
## Level 9-10:
In this challenge we need to find human readable **strings** with many **=** sings. We can use **strings** command and pipe it to **grep**. we can also only use the string command and figure out the password since it is mentioned that the password is next to =====. But it may cause cofusions hence we use the **grep** also.
```
strings data.txt | grep ===
```
#### password: G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
---
---
## Level 10-11:
Here we know that the password is base64 encoded. We can either copy the contents of the file and use an online base64 decoder or run the following command:
```
base64 -d data.txt
```
-d is for decoding... without that it made the password more worse...
#### password: 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
---
---
## Level 11-12:
Here the contents of the file is in Rot13 encoded. I used an online rot13 decipher.
#### password: JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
---
---
## Level 12-13:
For this challenge I seeked help form: https://mayadevbe.me/posts/overthewire/bandit/level13/
First we craeate a temporary directory in **/tmp** using **mktemp -d** and copy **data.txt** to it. Then we rename it as **hexdump_data** using the **mv** command. We will now revert the data to operate on the actual data using:
```
xxd -r hexdump_data compressed_data
```
Now we need to decompress. Now we rename compressed_data to compressed_data.gz and compress the file using **gzip**. When we run:
```
xxd compressed_data | head
```
we can see the file is not fully decompressed. Hence we use version 2 of **bzip** to decompress the file. But first we need to rename the file with **.bz** extention for the command to work:
```
mv compressed_data compressed_data.bz2
bzip2 -d compressed_data.bz2
```
running xxd again shows that it is still gzip compressed hence we rename the file and decompress again.
```
mv compressed_data compressed_data.gz
gzip -d compressed_data.gz
```
Using either **xxd compressed_data | head** we can see the **‘data5.bin’** string, which is a filename. **Head** command is used to see first 10 lines incase the folder is toooo big.
Now we rename and use **tar** to extract the file:
```
mv compressed_data compressed_data.tar
tar -xf compressed_data.tar
```
Now we extract **data6.bin** from **data5.bin**:
```
tar -xf data5.bin
```
again with **data6.bin** to **data8.bin**:
```
tar -xf data6.bin.out
```
**data8.bin** is COMPRESSED! hence we decompress it using gzip AGAIN!:
```
mv data8.bin data8.gz
gzip -d data8.gz
```
Now when we run **ls**  data8 is decompressed:
```
cat data8
```
we get the passsword.
#### password: wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
---
---
## Level 13-14:
Here we **cat** the **sshkey.private** and copy the private key. We exit and make a folder i our home directory and paste the password. We set the permissions of the folder to **chmod 700 key.private** and save the file using **vim** etc. Then we ssh into bandit 14:
```
ssh -i key.private bandit14@bandit.labs.overthewire.org -p 2220
```
we can cat the password for bandit14 in bandit14 itself for future refference.
#### password: fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
---
---
## Level 14-15:
In this level we need to submit the bandit14 password to localhost with port 30000. We use the **nc** command:
```
nc localhost 30000
```
and submit the password.
#### password: jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
---
---
## Level 15-16:
This challenge specifies that we need ssl encryption to log into localhost. WE can use **openssl s_client to implement ssl.
```
openssl s_client -connect localhost:30001
```
and submit current password.
#### password: jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
---
---
## Level 16-17:
In this we ca use **nmap** to discover how many servers ports run on localhost port 31000 to 32000.
```
nmap -sv localhost -p 31000-32000
```
Here we see that 2 ports are open with ssl encryption:31581 and 31790. We try to login to the ports and find that port 31790 is the legitimate one.
We send in the current password and it gives back a private key.
Now we create a file in bandit 16 itself and chmod it to 400.
```
chmod 400 key.private
ssh -i key.private bandit17@bandit.labs.overthewire.org -p 2220
```
#### password: JQttfApK4SeyHwDlI9SXGR50qclOAil1
---
---
## Level 17-18:
Here in this level we need to find the password which is in the passwords.new file and the password is the only difference between the files passwords.new and passwods.old. We can use the **diff** command which displays the difference between 2 files.
```
diff password.new password.old
```
Here since passwords.new is writted first, the first password is the correct one.
#### password: hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
---
---
## Level 18-19:
In this level there is a **.bashrc** file which runs every time we try to log in or when the terminal is loaded.
After searching the i found out we can ssh allows remote execution of commands. We simply add the command after the ssh expression. Hence we see what is in the bandit18 home directory. And then **cat** it.
```
ssh bandit18@bandit.labs.overthewire.org -p 2220 ls
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```
#### password: awhqfNnAbc1naukrpqDYcF95h7HoMTrC
---
---
## Level 19-20:
In this level we first need to check the ownership of the setuid binary. since the owner is bandit20 and group is bandit19, we can run the file as bandit20:
```
./bandit20-do
./bandit20-do ls /etc/bandit_pass
./bandit20-do cat /etc/bandit_pass/bandit20
```
#### password: VxCazJaVykI6W36BkBU0mJTCM8rR95XT
---
---
## Level 20-21:
Here in this level we need to create a server on localhost and run it in the background.
```_
echo -n 'VxCazJaVykI6W36BkBU0mJTCM8rR95XT' | nc -l -p 1234 &
./suconnect 1234
```
-n preventa newline charecter, -l is a listining port, -p specifies the port and & makes it run in the background.
For this level I took help from:
https://mayadevbe.me/posts/overthewire/bandit/level21/
#### password: NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
---
---
## Level 21-22:
In this we will first look in to **/etc/corn.d** and find the required **cronjob** for this level i.e. cronjob_bandit24.
cronjobs are programs running automatically at regular intervals. 
```
ls -la /etc/cron.d
```
now we can **cat** the required cronjob to take a look inside.
```
cat /etc/cron.d/cronjob_bandit22
```
Now we know that this paticular cronjob runs the cronjob_bandit22.sh file located in /usr/bin/cronjob_bandit22.sh.
```
cat /usr/bin/cronjob_bandit22.sh
```
now we know that there is a file named **t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv** in the /tmp directory. {I thought it was the password😅}
we simply **cat** that file and get the password.
#### password: WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff
---
---
## Level 22-23:
In this level we follow the previous steps: look into the /etc/cron.d/ using **ls -la**:
```
ls -ls
cat /etc/cron.d/cronjob_bandit23
cat /usr/bin/cronjob_bandit23.sh
```
After analysing the script we can see that there are 2 variables in the script: **myname** and **mytarget**.
the **myname** variable will take **whoami** as input (whoami is bandit23).The filename is created by the line **echo I am user $myname | md5sum | cut -d ' ' -f 1**. We need to replace **$myname** with **bandit23**.
```
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
```
now we get a file with (password like)name: 8ca319486bfbbc3663ea0fbe81326349 {Previous command gives us the file name}
```
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```
#### password: QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G
---
---
## Level 23-24:
We shall repeat the same steps and get into /etc/cron.d/:
```
ls -la
cat /etc/cron.d/cronjob_bandit24
cat /usr/bin/cronjob_bandit24.sh
```
Here we get a script... which does:  
### for i in * .*;    --> It starts a loop that reads all the files and directories in current directory.
### do    --> in loop  
### if [ "$i" != "." -a "$i" != ".." ];    --> It checks if the current item is not the current or parent directory.
### then    --> if it is so,
### echo "Handling $i"    --> It prints that script is handling the item.
### owner="$(stat --format "%U" ./$i)"    -->this line uses the stat command to get the owner(user) and stores it in the 
owner variable.
### if [ "${owner}" = "bandit23" ]; then    --> It checks if the owner of the particular item is bandit23.
### timeout -s 9 60 ./$i    --> It uses the timeout command to execute the current item and kills the execution if it lasts longer than 60 seconds.
### fi    --> It marks the end of the if statement.
### rm -f ./$i    --> This line deletes the current item forcefully without asking for permission.
### fi    --> End of if statement
### done    --> End of loop  
it basically runs through each object, runs and deletes it.  
hence we need to write ascript that takes the password from the file to another file before it gets deleted.
```
touch /tmp/getpswd.sh
vim /tmp/getpswd.sh
```
write in the file:  
```
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/s8n.txt
```
Change permissions and execute:
```
chmod 777 /tmp/getpswd.sh
touch /tmp/s8n.txt
chmod 666 /tmp/s8n.txt
cp /tmp/getpswd.sh /var/spool/bandit24/foo
```
wait for a while:
```
cat /tmp/s8n.txt
```
#### password: VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar
---
---
## Level 24-25:
In this level to brute force through the 4 digit code we shall first create a folder in a temporary directory.
```
mktemp -d
vim brute.sh
```
In this executable file we shall write the script. In the script i have written, I made the script give the current password and the 4 digit pin from 5000-9999 {After many trail and error I found out that the password does not come untill 5062-somethig... so I shortened the loop or else my computer was not able to process it...} and then it displays it on the terminal. After the password is retrived, the loop ends:
```
#!/bin/bash

for i in {5000..9999}
do
        echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i"
done  | nc localhost 30002
```
#### password: p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d
---
---
---

