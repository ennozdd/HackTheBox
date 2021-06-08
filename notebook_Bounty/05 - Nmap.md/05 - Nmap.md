# 05 - Nmap

```sql
# Nmap 7.91 scan initiated Sat Jun  5 15:21:34 2021 as: nmap -sC -sV -p- -oN nmap/bounty 10.10.10.93
Nmap scan report for 10.10.10.93
Host is up (0.066s latency).
Not shown: 65534 filtered ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 7.5
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/7.5
|_http-title: Bounty
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Jun  5 15:23:30 2021 -- 1 IP address (1 host up) scanned in 115.43 seconds
```