# 10 - SMB


```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham]
└──╼ $ smbmap -H 10.10.10.130 -u 'guest'
[+] IP: 10.10.10.130:445        Name: 10.10.10.130                                      
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        ADMIN$                                                  NO ACCESS       Remote Admin
        BatShare                                                READ ONLY       Master Wayne's secrets
        C$                                                      NO ACCESS       Default share
        IPC$                                                    READ ONLY       Remote IPC
        Users                                                   READ ONLY
```


# Mount the shares
```bash
┌─[user@parrot]─[10.10.14.18]─[/mnt/arkham]
└──╼ $ sudo mount -t cifs -o user='guest',pass='' //10.10.10.130/BatShare BatShare/
┌─[user@parrot]─[10.10.14.18]─[/mnt/arkham]
└──╼ $ sudo mount -t cifs -o user='guest',pass='' //10.10.10.130/Users Users/
```


# appserver.zip
```bash
┌─[user@parrot]─[10.10.14.18]─[/mnt/arkham/BatShare]
└──╼ $ ls -la
total 3952
drwxr-xr-x 2 root root       0 Feb  3  2019 .
drwxr-xr-x 1 root root      26 Jul 22 15:05 ..
-rwxr-xr-x 1 root root 4046695 Feb  1  2019 appserver.zip
```


```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham/appserver]
└──╼ $ unzip appserver.zip 
Archive:  appserver.zip
  inflating: IMPORTANT.txt           
  inflating: backup.img              
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham/appserver]
└──╼ $ ls
appserver.zip  backup.img  IMPORTANT.txt
```

# LUKS encrypted file
```
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham/appserver]
└──╼ $ file backup.img 
backup.img: LUKS encrypted file, ver 1 [aes, xts-plain64, sha256] UUID: d931ebb1-5edc-4453-8ab1-3d23bb85b38e
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham/appserver]
└──╼ $ cat IMPORTANT.txt 
Alfred, this is the backup image from our linux server. Please see that The Joker or anyone else doesn't have unauthenticated access to it. - Bruce 
```


# [Cracking LUKS](https://hackernoon.com/cracking-linux-full-disc-encryption-luks-with-hashcat-832d5543101f)

# Header

```
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham/appserver]
└──╼ $ cryptsetup luksDump backup.img 
LUKS header information for backup.img

Version:        1
Cipher name:    aes
Cipher mode:    xts-plain64
Hash spec:      sha256
Payload offset: 4096
MK bits:        256
MK digest:      9a 35 ab 3d b2 fe 09 d6 5a 92 bd 01 50 35 a6 ab dc ea 01 47 
MK salt:        36 e8 8d 00 2f b0 3c 1f de 4d 9d 7b a6 9c 59 25 
                7a e7 1d d7 89 3d 9c ab ef b6 09 8c a8 7b 87 13 
MK iterations:  176409
UUID:           d931ebb1-5edc-4453-8ab1-3d23bb85b38e

Key Slot 0: ENABLED
        Iterations:             2822546
        Salt:                   3a db 8d 4b 9b f1 63 61 1b df a9 76 16 77 30 96 
                                5c 32 a9 aa e4 e7 9d cf 4e f5 9b 3f a1 4c 27 2f 
        Key material offset:    8
        AF stripes:             4000
Key Slot 1: DISABLED
Key Slot 2: DISABLED
Key Slot 3: DISABLED
Key Slot 4: DISABLED
Key Slot 5: DISABLED
Key Slot 6: DISABLED
Key Slot 7: DISABLED

```


# Extract header and bruteforce it
```
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham/appserver]
└──╼ $ dd if=backup.img of=luks-header bs=1024 count=4097
4097+0 records in
4097+0 records out
4195328 bytes (4.2 MB, 4.0 MiB) copied, 0.0104315 s, 402 MB/s
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham/appserver]
└──╼ $ hashcat -m 14600 -a 0  luks-header  /usr/share/wordlists/rockyou.txt
password: batmanforever
```

# Set up a loop interface for mounting
```
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham/appserver]
└──╼ $ sudo losetup -P -f backup.img 
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham/appserver]
└──╼ $ lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0    7:0    0   13M  0 loop 
sda      8:0    0  128G  0 disk 
└─sda1   8:1    0  128G  0 part /home
sr0     11:0    1 1024M  0 rom  
```

# Decrypt the luks device 
```
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham/appserver]
└──╼ $ sudo cryptsetup luksOpen /dev/loop0 luks
Enter passphrase for /home/user/htb/arkham/appserver/backup.img: 
┌─[user@parrot]─[10.10.14.18]─[~/htb/arkham/appserver]
└──╼ $ lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
loop0    7:0    0   13M  0 loop  
└─luks 252:0    0   11M  0 crypt 
sda      8:0    0  128G  0 disk  
└─sda1   8:1    0  128G  0 part  /home
sr0     11:0    1 1024M  0 rom   
```

# Mount the luks partition

```
┌─[user@parrot]─[10.10.14.18]─[/dev/mapper]
└──╼ $ sudo mount /dev/mapper/luks /mnt/luks/
┌─[user@parrot]─[10.10.14.18]─[/dev/mapper]
└──╼ $ cd /mnt/luks/;ls
lost+found  Mask
```


# org.apache.myfaces.SECRET
```xml
┌─[user@parrot]─[10.10.14.18]─[/mnt/luks/Mask/tomcat-stuff]
└──╼ $ cat web.xml.bak  |head -n34
<param-name>org.apache.myfaces.SECRET</param-name>
<param-value>SnNGOTg3Ni0=</param-value>
```

  
# Decoded secret
```
┌─[user@parrot]─[10.10.14.18]─[/mnt/luks/Mask/tomcat-stuff]
└──╼ $ echo -n SnNGOTg3Ni0= |base64 -d
JsF9876-
```


