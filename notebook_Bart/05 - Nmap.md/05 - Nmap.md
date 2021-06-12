# 05 - Nmap


```sql
# Nmap 7.91 scan initiated Fri Jun 11 12:54:21 2021 as: nmap -sC -sV -p- -oN nmap/bart 10.10.10.81
Nmap scan report for 10.10.10.81
Host is up (0.067s latency).
Not shown: 65534 filtered ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: Did not follow redirect to http://forum.bart.htb/
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Jun 11 12:56:16 2021 -- 1 IP address (1 host up) scanned in 115.49 seconds
```