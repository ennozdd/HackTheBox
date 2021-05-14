# Initial Enumeration

```sql
# Nmap 7.91 scan initiated Wed May 12 14:36:03 2021 as: nmap -sC -sV -p- -v -oA nmap/bashed 10.10.10.68
Nmap scan report for 10.10.10.68
Host is up (0.079s latency).
Not shown: 65534 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-favicon: Unknown favicon MD5: 6AA5034A553DFA77C3B2C7B4C26CF870
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Arrexel's Development Site

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed May 12 14:40:29 2021 -- 1 IP address (1 host up) scanned in 265.90 seconds
```
