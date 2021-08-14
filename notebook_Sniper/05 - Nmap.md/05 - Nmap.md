# 05 - Nmap

```sql
# Nmap 7.91 scan initiated Fri Aug 13 15:21:30 2021 as: nmap -sC -sV -p- -oA nmap/sniper -vvv 10.10.10.151
Nmap scan report for 10.10.10.151
Host is up, received echo-reply ttl 127 (0.074s latency).
Scanned at 2021-08-13 15:21:31 +03 for 214s
Not shown: 65530 filtered ports
Reason: 65530 no-responses
PORT      STATE SERVICE       REASON          VERSION
80/tcp    open  http          syn-ack ttl 127 Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: Sniper Co.
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 127
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: 7h00m00s
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 51578/tcp): CLEAN (Timeout)
|   Check 2 (port 18459/tcp): CLEAN (Timeout)
|   Check 3 (port 51336/udp): CLEAN (Timeout)
|   Check 4 (port 47014/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-08-13T19:24:30
|_  start_date: N/A

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Aug 13 15:25:05 2021 -- 1 IP address (1 host up) scanned in 214.27 seconds
```