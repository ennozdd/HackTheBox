# 05 - Enumeration


```sql
# Nmap 7.91 scan initiated Tue Jun  1 18:28:10 2021 as: nmap -sC -sV -p- -oA nmap/tartarsauce 10.10.10.88
Nmap scan report for 10.10.10.88
Host is up (0.067s latency).
Not shown: 65534 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 5 disallowed entries 
| /webservices/tar/tar/source/ 
| /webservices/monstra-3.0.4/ /webservices/easy-file-uploader/ 
|_/webservices/developmental/ /webservices/phpmyadmin/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Landing Page

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Jun  1 18:29:02 2021 -- 1 IP address (1 host up) scanned in 51.27 seconds
```