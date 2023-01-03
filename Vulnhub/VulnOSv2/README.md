# VulnOSv2

Starting off I nmaped the box with
`nmap -sVC 192.168.56.104`
![flag Announcement Image]([https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/main/.png](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/main/Vulnhub/VulnOSv2/VulnOSv2%20Images/image1.png))

After that, I looked around at the website



After that, I clicked on the link. Looking around I could not find anything that was of value so i checked searchsploit for drupal since I saw that as the icon.



Looking around i noticed drupalgeddon2 which has worked for me in the past.



after install highline i ran drupalgeddon2 and got in as www-data



I checked what version of ubuntu we were on and it is ANCIENT!!



so fun time "DiRtY cOw"





Once I couldn't get to /tmp i decided to use metasploit



grabbed my exploit.cpp and found out it worked the first time but would not let me go into the /tmp folder.



ran final g++ in the dirty cow file.

`g++ -Wall -pedantic -O2 -std=c++11 -pthread -o dcow exploit.cpp -lutil`




