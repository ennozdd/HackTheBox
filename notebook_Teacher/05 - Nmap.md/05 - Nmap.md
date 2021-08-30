# 05 - Nmap


```sql
# Nmap 7.91 scan initiated Sat Aug 28 15:06:04 2021 as: nmap -sC -sV -p- -oA nmap/teacher -vvv 10.10.10.153
Nmap scan report for 10.10.10.153
Host is up, received echo-reply ttl 63 (0.062s latency).
Scanned at 2021-08-28 15:06:05 +03 for 97s
Not shown: 65534 closed ports
Reason: 65534 resets
PORT   STATE SERVICE REASON         VERSION
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.25 ((Debian))
| http-methods: 
|_  Supported Methods: POST OPTIONS HEAD GET
|_http-server-header: Apache/2.4.25 (Debian)
|_http-title: Blackhat highschool

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Aug 28 15:07:42 2021 -- 1 IP address (1 host up) scanned in 97.99 seconds
```


There is only http hosted on this box. 