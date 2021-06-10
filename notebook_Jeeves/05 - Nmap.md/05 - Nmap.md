# 05 - Nmap


```sql
# Nmap 7.91 scan initiated Wed Jun  9 20:15:40 2021 as: nmap -vvv -p- -sC -sV -oA nmap/ 10.10.10.63
Nmap scan report for 10.10.10.63
Host is up, received echo-reply ttl 127 (0.069s latency).
Scanned at 2021-06-09 20:15:40 +03 for 153s
Not shown: 65531 filtered ports
Reason: 65531 no-responses
PORT      STATE SERVICE      REASON          VERSION
80/tcp    open  http         syn-ack ttl 127 Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: Ask Jeeves
135/tcp   open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
445/tcp   open  microsoft-ds syn-ack ttl 127 Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
50000/tcp open  http         syn-ack ttl 127 Jetty 9.4.z-SNAPSHOT
|_http-server-header: Jetty(9.4.z-SNAPSHOT)
|_http-title: Error 404 Not Found
Service Info: Host: JEEVES; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 5h07m07s, deviation: 0s, median: 5h07m06s
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 55172/tcp): CLEAN (Timeout)
|   Check 2 (port 9219/tcp): CLEAN (Timeout)
|   Check 3 (port 36896/udp): CLEAN (Timeout)
|   Check 4 (port 48293/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-06-09T22:24:44
|_  start_date: 2021-06-09T22:21:19

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Jun  9 20:18:14 2021 -- 1 IP address (1 host up) scanned in 153.77 seconds
```