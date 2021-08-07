# 05 - Nmap

```sql
# Nmap 7.91 scan initiated Fri Aug  6 12:11:47 2021 as: nmap -sC -sV -p- -oA nmap/access -vvv 10.10.10.98
Nmap scan report for 10.10.10.98
Host is up, received echo-reply ttl 127 (0.079s latency).
Scanned at 2021-08-06 12:11:47 +03 for 372s
Not shown: 65532 filtered ports
Reason: 65532 no-responses
PORT   STATE SERVICE REASON          VERSION
21/tcp open  ftp     syn-ack ttl 127 Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV failed: 425 Cannot open data connection.
| ftp-syst: 
|_  SYST: Windows_NT
23/tcp open  telnet? syn-ack ttl 127
80/tcp open  http    syn-ack ttl 127 Microsoft IIS httpd 7.5
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/7.5
|_http-title: MegaCorp
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Aug  6 12:17:59 2021 -- 1 IP address (1 host up) scanned in 372.88 seconds
```



