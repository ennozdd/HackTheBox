# 05 - Nmap

```sql
# Nmap 7.91 scan initiated Sat Aug  7 13:25:28 2021 as: nmap -sC -sV -p- -oA nmap/fuse -vvv 10.10.10.193
Nmap scan report for 10.10.10.193
Host is up, received echo-reply ttl 127 (0.084s latency).
Scanned at 2021-08-07 13:25:28 +03 for 466s
Not shown: 65515 filtered ports
Reason: 65515 no-responses
PORT      STATE SERVICE      REASON          VERSION
53/tcp    open  domain       syn-ack ttl 127 Simple DNS Plus
80/tcp    open  http         syn-ack ttl 127 Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: Site doesn't have a title (text/html).
88/tcp    open  kerberos-sec syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2021-08-07 10:52:29Z)
135/tcp   open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn  syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap         syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: fabricorp.local, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds syn-ack ttl 127 Windows Server 2016 Standard 14393 microsoft-ds (workgroup: FABRICORP)
464/tcp   open  kpasswd5?    syn-ack ttl 127
593/tcp   open  ncacn_http   syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped   syn-ack ttl 127
3268/tcp  open  ldap         syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: fabricorp.local, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped   syn-ack ttl 127
5985/tcp  open  http         syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf       syn-ack ttl 127 .NET Message Framing
49666/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
49667/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
49675/tcp open  ncacn_http   syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49676/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
49679/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
49698/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
Service Info: Host: FUSE; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 2h40m46s, deviation: 4h02m30s, median: 20m45s
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 21069/tcp): CLEAN (Timeout)
|   Check 2 (port 62199/tcp): CLEAN (Timeout)
|   Check 3 (port 15988/udp): CLEAN (Timeout)
|   Check 4 (port 55519/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: Fuse
|   NetBIOS computer name: FUSE\x00
|   Domain name: fabricorp.local
|   Forest name: fabricorp.local
|   FQDN: Fuse.fabricorp.local
|_  System time: 2021-08-07T03:53:21-07:00
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2021-08-07T10:53:22
|_  start_date: 2021-08-07T10:45:07

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Aug  7 13:33:14 2021 -- 1 IP address (1 host up) scanned in 466.92 seconds
```

We are looking at a Domain Controller, there are many services we can enumerate. Furthermore, WinRM (5985) is open, if we can manage to steal credentials, we can log in with evil-winrm. It's advisable to start off with the http service because it has the most attack surface. Of course, it goes without saying that nmap reveals also the domain name `fabricorp.local`