# VulnOSv2

## fun rating 7/10
## difficulty 3/10

Starting off I nmaped the box with

```nmap -sVC 192.168.56.104```

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/26b30ae59f711928ee3a0bf4900abaf3ac5e4fb9/Vulnhub/VulnOSv2/VulnOSv2%20Images/1.png)

After that, I looked around at the website and used gobuster to find any other links. I could not find anything.

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/26b30ae59f711928ee3a0bf4900abaf3ac5e4fb9/Vulnhub/VulnOSv2/VulnOSv2%20Images/2.png)

After that, I clicked on the link. Looking around I could not find anything that was of value so i checked searchsploit for drupal since I saw that as the icon.

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/26b30ae59f711928ee3a0bf4900abaf3ac5e4fb9/Vulnhub/VulnOSv2/VulnOSv2%20Images/3.png)

Looking around i noticed drupalgeddon2 which has worked for me in the past.

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/26b30ae59f711928ee3a0bf4900abaf3ac5e4fb9/Vulnhub/VulnOSv2/VulnOSv2%20Images/4.png)

after install highline i ran drupalgeddon2 and got in as www-data

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/26b30ae59f711928ee3a0bf4900abaf3ac5e4fb9/Vulnhub/VulnOSv2/VulnOSv2%20Images/5.png)

I checked what version of ubuntu we were on and it is ANCIENT!!

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/26b30ae59f711928ee3a0bf4900abaf3ac5e4fb9/Vulnhub/VulnOSv2/VulnOSv2%20Images/7.png)

so fun time "DiRtY cOw"

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/26b30ae59f711928ee3a0bf4900abaf3ac5e4fb9/Vulnhub/VulnOSv2/VulnOSv2%20Images/8.png)



Once I couldn't get to /tmp i decided to use metasploit

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/26b30ae59f711928ee3a0bf4900abaf3ac5e4fb9/Vulnhub/VulnOSv2/VulnOSv2%20Images/9.png)

grabbed my exploit.cpp and found out it worked the first time but would not let me go into the /tmp folder.

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/26b30ae59f711928ee3a0bf4900abaf3ac5e4fb9/Vulnhub/VulnOSv2/VulnOSv2%20Images/10.png)

ran final g++ in the dirty cow file.

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/26b30ae59f711928ee3a0bf4900abaf3ac5e4fb9/Vulnhub/VulnOSv2/VulnOSv2%20Images/11.png)

`g++ -Wall -pedantic -O2 -std=c++11 -pthread -o dcow exploit.cpp -lutil`

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/26b30ae59f711928ee3a0bf4900abaf3ac5e4fb9/Vulnhub/VulnOSv2/VulnOSv2%20Images/12.png)
