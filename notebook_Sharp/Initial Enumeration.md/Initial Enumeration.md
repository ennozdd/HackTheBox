# Initial Enumeration


# Nmap
```sql
kali㉿kali)-[10.10.14.131/23]-[~/htb/sharp]
└─$ cat nmap/.nmap 
# Nmap 7.91 scan initiated Sat Apr 17 16:23:00 2021 as: nmap -sS -sC -sV -p- -v -oA nmap/ 10.10.10.219
Nmap scan report for 10.10.10.219
Host is up (0.081s latency).
Not shown: 65529 filtered ports
PORT     STATE SERVICE              VERSION
135/tcp  open  msrpc                Microsoft Windows RPC
139/tcp  open  netbios-ssn          Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds?
5985/tcp open  http                 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
8888/tcp open  msexchange-logcopier Microsoft Exchange 2010 log copier
8889/tcp open  mc-nmf               .NET Message Framing
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: -50m56s
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-04-17T12:39:27
|_  start_date: N/A

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Apr 17 16:30:59 2021 -- 1 IP address (1 host up) scanned in 478.92 seconds
```