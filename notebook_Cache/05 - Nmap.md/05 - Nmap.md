# 05 - Nmap


```sql
# Nmap 7.91 scan initiated Tue Sep  7 18:52:21 2021 as: nmap -sC -sV -p- -oA nmap/cache -vvv 10.10.10.188
Nmap scan report for 10.10.10.188
Host is up, received echo-reply ttl 63 (0.097s latency).
Scanned at 2021-09-07 18:52:22 +03 for 364s
Not shown: 65533 closed ports
Reason: 65533 resets
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 a9:2d:b2:a0:c4:57:e7:7c:35:2d:45:4d:db:80:8c:f1 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCb3lyySrN6q6RWe0mdRQOvx8TgDiFAVhicR1h3UlBANr7ElILe7ex89jpzZSkhrYgCF7iArq7PFSX+VY52jRupsYJp7V2XLY9TZOq6F7u6eqsRA60UVeqkh+WnTE1D1GtQSDM2693/1AAFcEMhcwp/Z7nscp+PY1npxEEP6HoCHnf4h4p8RccQuk4AdUDWZo7WlT4fpW1oJCDbt+AOU5ylGUW56n4uSUG8YQVP5WqSspr6IY/GssEw3pGvRLnoJfHjARoT93Fr0u+eSs8zWhpHRWkTEWGhWIt9pPI/pAx2eAeeS0L5knZrHppoOjhR/Io+m0i1kF1MthV+qYjDjscf
|   256 bc:e4:16:3d:2a:59:a1:3a:6a:09:28:dd:36:10:38:08 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBFAHWTqc7a2Az0RjFRBeGhfQkpQrBmEcMntikVFn2frnNPZklPdV7RCy2VW7Ae+LnyJU4Nq2LYqp2zfps+BZ3H4=
|   256 57:d5:47:ee:07:ca:3a:c0:fd:9b:a8:7f:6b:4c:9d:7c (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMnbsx7/pCTUKU7WwHrL/d0YS9c99tRraIPvg5zrRpiF
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.29 ((Ubuntu))
| http-methods: 
|_  Supported Methods: HEAD GET POST OPTIONS
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Cache
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Sep  7 18:58:26 2021 -- 1 IP address (1 host up) scanned in 364.80 seconds
```

Only two ports are open. With verbose openssh we can only google and find the ubuntu version. Other than that there is not much we can tell.  **4ubuntu0.3** gives us the exact version information, that is Ubuntu 18.04. See the screenshot below.


![](vx_images/4700338250276.png)