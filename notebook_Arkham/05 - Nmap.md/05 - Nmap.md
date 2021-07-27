# 05 - Nmap


```sql
# Nmap 7.91 scan initiated Thu Jul 22 15:01:53 2021 as: nmap -sC -sV -p- -oA nmap/arkham -vvv 10.10.10.130
Nmap scan report for 10.10.10.130
Host is up, received echo-reply ttl 127 (0.084s latency).
Scanned at 2021-07-22 15:01:53 +03 for 465s
Not shown: 65528 filtered ports
Reason: 65528 no-responses
PORT      STATE SERVICE       REASON          VERSION
80/tcp    open  http          syn-ack ttl 127 Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 127
8080/tcp  open  http          syn-ack ttl 127 Apache Tomcat 8.5.37
| http-methods: 
|   Supported Methods: GET HEAD POST PUT DELETE OPTIONS
|_  Potentially risky methods: PUT DELETE
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Mask Inc.
49666/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: 7m34s
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 29094/tcp): CLEAN (Timeout)
|   Check 2 (port 57596/tcp): CLEAN (Timeout)
|   Check 3 (port 8458/udp): CLEAN (Timeout)
|   Check 4 (port 22737/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-07-22T12:16:37
|_  start_date: N/A

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Jul 22 15:09:38 2021 -- 1 IP address (1 host up) scanned in 465.00 seconds
```