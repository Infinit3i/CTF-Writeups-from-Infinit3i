# Venom: 1

## fun rating 8/10
## difficulty 4/10

TLDR: `nmap > HTTP source code > decrypt md5 > ftp grab > decode vigenere cipher > host virtualization > subrion exploit on /panel > reverse .phar in uploads > find hidden file > sudo to root`

Nmap box with 
```nmap -sVC 192.168.56.103```

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/1.png)

Found ftp, http, smb, and HTTPS
Trying FTP with anonymous/anonymous does not work. Looking around HTTP.
The bottom of the page source has some valuable information.

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/2.png)

Decrypting the MD5 got me hostinger

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/3.png)

After that we use hostinger as username and password for FTP.

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/4.png)

We grab the hint.txt file. Reading what it says

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/5.png)

```T0D0 --

* You need to follow the 'hostinger' on WXpOU2FHSnRVbWhqYlZGblpHMXNibHBYTld4amJWVm5XVEpzZDJGSFZuaz0= also aHR0cHM6Ly9jcnlwdGlpLmNvbS9waXBlcy92aWdlbmVyZS1jaXBoZXI=
* some knowledge of cipher is required to decode the dora password..
* try on venom.box
password -- L7f9l8@J#p%Ue+Q1234 -> deocode this you will get the administrator password 


Have fun .. :)
```

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/6.png)

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/7.png)

```https://cryptii.com/pipes/vigenere-cipher```

Follow to the website with the information provided.

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/8.png)

Received `E7r9t8@Q#h%Hy+M1234` from the vigenere cipher

Add venom.box to /etc/hosts

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/9.png)

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/10.png)

We see it is subrion 4.2

Type in `subrion 4.2 exploit` on google, and we receive [exploit](https://www.exploit-db.com/exploits/49876)
We go to /panel on website

`http://venom.box/panel/`

Login `dora/E7r9t8@Q#h%Hy+M1234`

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/11.png)

Have  [Shell](https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php) in /opt folder and upload with .phar extension
-switch your ip and port on .phar file
Run the shell.phar file on venom.box/uploads/shell.phar

With netcat reverse shell listening at 

`nc -lvnp 4444`

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/12.png)

Elevate tty
`python3 -c ‘import pty;pty.spawn(“/bin/bash”)’`
Su hostinger/hostinger

Looking around for configuration files or backup files, we find `/var/www/html/subrion/backup/.htaccess`

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/13.png)

Use `FzN+f2-rRaBgvALzj*Rk#_JJYfg8XfKhxqB82x_a` as nathan’s password

`Su nathan/FzN+f2-rRaBgvALzj*Rk#_JJYfg8XfKhxqB82x_a`

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/14.png)

Once root go into /root and open `cat /root/root.txt`

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/3c07c55f0a80e3161900aac2c021008082c394ed/Vulnhub/VENOM:%201/VENOM:%201%20Images/15.png)

Thanks for reading!
Check out my [website](https://www.matthewiver.com)
