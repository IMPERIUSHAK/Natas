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

