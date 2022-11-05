### Cvg3n3rat0r

Points: 102
Solves: 38

Ever wanted to get hired by your favourite E-corp? Generate your brand new CV and get hired every time.

BTW, have you ever heard the joke about putting your resume on the bosses computer? While that's probably a bad idea, grabbing the flag from /flag.txt
most definitely isn't!

Now with W3schools support!

http://cvgenerator.zajebistyc.tf

I knew the atack that was needed was xss but i needed to find out how to exploit the system. The first few lines were <p> paragraph tags with <b> bold inside of them. I used my previous knowledge to inject <script> tags. I realized that document.location.href was needed so i added that. I was then given the /tmp directory it was located in.
  
<script>document.write(document.location.href)</script>

  I found a medium article by r3d-buck3t to exfil xss
  
  https://medium.com/r3d-buck3t/xss-to-exfiltrate-data-from-pdfs-f5bbb35eaba7
  
  after slowly looking around the page i noticed one i thought would work.
  
```  
<script>x=new XMLHttpRequest;x.onload=function(){document.write(this.responseText)};x.open("GET","file:///home/reader/.ssh/id_rsa");x.send();</script>
```  
  
  I switched the file path to what i needed which was "file:///flag.txt"
  
  After 20 attempts I finally achieved my answer.
