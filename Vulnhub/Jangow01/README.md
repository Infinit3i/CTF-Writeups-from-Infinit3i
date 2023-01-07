# Jangow01

[Vulnhub Jangow01](https://www.vulnhub.com/entry/jangow-101,754/)

## fun rating 5/10
## difficulty 2/10

Nmap box with 
`nmap -sVC 192.168.56.118`

Once I saw FTP I tried to log on with anonymous/anonymous

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/4d1c945e9c31f448b8a22b18bd94624acbf0003b/Vulnhub/Jangow01/Jangow01%20Images/1.png)

We then visit the website on port 80

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/4d1c945e9c31f448b8a22b18bd94624acbf0003b/Vulnhub/Jangow01/Jangow01%20Images/2.png)

Once on the website we see some tabs on the top, visit buscar and see = at the end of the uri. we try to input some information into it.

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/4d1c945e9c31f448b8a22b18bd94624acbf0003b/Vulnhub/Jangow01/Jangow01%20Images/3.png)

It works when we use id!

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/4d1c945e9c31f448b8a22b18bd94624acbf0003b/Vulnhub/Jangow01/Jangow01%20Images/4.png)

We look around the system and we can view /home/jangow01/user.txt

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/4d1c945e9c31f448b8a22b18bd94624acbf0003b/Vulnhub/Jangow01/Jangow01%20Images/5.png)

Looking around for a config or backup file, we use ls -alt and find hidden files in our orginal folder

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/4d1c945e9c31f448b8a22b18bd94624acbf0003b/Vulnhub/Jangow01/Jangow01%20Images/6.png)

We then log into ftp with the jangow01/abygurl69

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/4d1c945e9c31f448b8a22b18bd94624acbf0003b/Vulnhub/Jangow01/Jangow01%20Images/7.png)

Once on the box we find a directory where we can upload files. We found out we can upload them to /home/jangow01

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/4d1c945e9c31f448b8a22b18bd94624acbf0003b/Vulnhub/Jangow01/Jangow01%20Images/8.png)

Looking at the version of ubuntu we see it is older just like the [VulnOSv2](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/2d018642452f5c5e4e615b08f2b010d5dfafbb1f/Vulnhub/VulnOSv2/README.md) box. We use this [exploit](https://www.exploit-db.com/exploits/45010).

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/4d1c945e9c31f448b8a22b18bd94624acbf0003b/Vulnhub/Jangow01/Jangow01%20Images/9.png)

We log on to the actual virtualbox of jangow01 now that we know the login and password

we login with jangow01/abygurl69

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/4d1c945e9c31f448b8a22b18bd94624acbf0003b/Vulnhub/Jangow01/Jangow01%20Images/10.png)

gcc file and run. Once the file is run it will give a root shell where you can maneuver to /root

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/4d1c945e9c31f448b8a22b18bd94624acbf0003b/Vulnhub/Jangow01/Jangow01%20Images/11.png)

We finished another vulnhub box!
