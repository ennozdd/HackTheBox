# 05 - Nmap



```sql
# Nmap 7.91 scan initiated Mon Jul 19 14:04:24 2021 as: nmap -sC -sV -p- -oA nmap/celestial -vvv -Pn 10.10.10.85
Nmap scan report for 10.10.10.85
Host is up, received user-set (0.089s latency).
Scanned at 2021-07-19 14:04:24 +03 for 85s
Not shown: 65534 closed ports
Reason: 65534 resets
PORT     STATE SERVICE REASON         VERSION
3000/tcp open  http    syn-ack ttl 63 Node.js Express framework
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Site doesn't have a title (text/html; charset=utf-8).

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Jul 19 14:05:49 2021 -- 1 IP address (1 host up) scanned in 85.49 seconds
```