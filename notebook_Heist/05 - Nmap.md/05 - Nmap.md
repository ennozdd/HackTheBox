# 05 - Nmap



```sql
# Nmap 7.91 scan initiated Wed Aug  4 14:35:08 2021 as: nmap -sC -sV -p- -oA nmap/heist -vvv 10.10.10.149
Nmap scan report for 10.10.10.149
Host is up, received echo-reply ttl 127 (0.073s latency).
Scanned at 2021-08-04 14:35:09 +03 for 297s
Not shown: 65530 filtered ports
Reason: 65530 no-responses
PORT      STATE SERVICE       REASON          VERSION
80/tcp    open  http          syn-ack ttl 127 Microsoft IIS httpd 10.0
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
| http-title: Support Login Page
|_Requested resource was login.php
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
445/tcp   open  microsoft-ds? syn-ack ttl 127
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49669/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: 7m42s
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 15305/tcp): CLEAN (Timeout)
|   Check 2 (port 48515/tcp): CLEAN (Timeout)
|   Check 3 (port 25486/udp): CLEAN (Timeout)
|   Check 4 (port 5774/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-08-04T11:47:12
|_  start_date: N/A

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Aug  4 14:40:06 2021 -- 1 IP address (1 host up) scanned in 298.06 seconds
```