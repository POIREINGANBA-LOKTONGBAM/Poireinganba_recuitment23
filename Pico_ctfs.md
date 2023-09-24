# !:PICO CTF:!
---
---
---
## Power Cookie:
In this challenge we have to modify the cookie.  
1. we visit the webpage given in the challenge.  
2. we use **inspect** to get into the source of the website.  
3. we go into **storage** in dev tools and o to cookies drop down menue.  
4. we edit the cookie value(admin) from 0 to 1.  
5. reload the age and get the flag.
#### flag: picoCTF{gr4d3_A_c00k13_5d2505be}
---
---
## SQL Direct:
For this challenge we have to login to the PostgreSQL server:
1. go to terminal and type in the link: psql -h saturn.picoctf.net -p 63373 -U postgres pico .
2. Show the tables using **\dt** command.
3. select the **'flags'** table using: **select * from flags;**
4. get the flag.
#### flag: picoCTF{L3arN_S0m3_5qL_t0d4Y_73b0678f}
---
---
## Java Code Analysis:
For this challenge we need to study the source code of the given website:
1. first we download the source code and search for **SecretGenerator** file inbookshelf-pico.zip\src\main\java\io\github\nandandesai\pico\security
2. Now we know that the secret key is **1234**.
3. Head over to the website and login.
4. use **inspect** to opean dev tools.
5. In the **Storage** section go to local storage
6. Select the jwt token in **auth-token**
7. decode the jwt using a website and the secret key.
8. adjust the values of role and email and set userId to 2.
9. copy the new jwt code and paste it in **Storage** over the old one.
10. change the **token payload** properties accordingly.
11. reload and select the **flag** book.
12. get the flag.
#### flag: picoCTF{w34k_jwt_n0t_g00d_d7c2e335}
---
---
## Irish Name Repo 1:
For this challenge, we will be using sql injection tecniques.
1. Go to the website and enter menue- Admin login.
2. Put username as random.
3. We can use **' or'1'='1** sql injection to get the flag.
   Here *' or'1'='1*  takes all the users from the database and sends it back. here since 1=1 is always true, it loggs in.
4. get the flag.
#### flag: picoCTF{s0m3_SQL_c218b685}
---
---
## Irish Name Repo 2:
For this challenge we can use a slightly different approach.
1. Go to website and enter menue- Admin login.
2. this time we will use **; --**
3. This sql injection comments out the rest of the querry and lets us in.(Since comments are usually ignored by most languages)
4. get the flag.
#### flag: picoCTF{m0R3_SQL_plz_fa983901}
---
---
## Irish Name Repo 3:
For this challenge we need to see the page source of the website:
1. Go to website and enter menue- Admin login.
2. Right click and select View page source.
3. Here we can see that there is a hidden debug with value zero(false). Also we can login using **.php** using **POST** method.
```
wget https://jupiter.challenges.picoctf.org/problem/29132/login.php --post-data="debug=1&password=abcdefghijklmnopqrstuvwxyz"
cat login.php
```
4. Here we will get an idea that the password is ROT13 encoded.
5. Hence we now can use rot13 to get the value of **'or'1'=1'** which is **a'be'1'='1**:
```
wget https://jupiter.challenges.picoctf.org/problem/29132/login.php --post-data="debug=1&password=a'be'1'='1"
cat login.php.1
```
6. Get the flag.
#### flag: picoCTF{3v3n_m0r3_SQL_06a9db19}
---
---
---
