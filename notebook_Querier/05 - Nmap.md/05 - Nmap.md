# 05 - Nmap


```sql
# Nmap 7.91 scan initiated Tue Aug 17 12:24:46 2021 as: nmap -sC -sV -p- -oA nmap/querier -vvv 10.10.10.125
Nmap scan report for 10.10.10.125
Host is up, received reset ttl 127 (0.077s latency).
Scanned at 2021-08-17 12:24:47 +03 for 131s
Not shown: 65521 closed ports
Reason: 65521 resets
PORT      STATE SERVICE       REASON          VERSION
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 127
1433/tcp  open  ms-sql-s      syn-ack ttl 127 Microsoft SQL Server 2017 14.00.1000.00; RTM
| ms-sql-ntlm-info: 
|   Target_Name: HTB
|   NetBIOS_Domain_Name: HTB
|   NetBIOS_Computer_Name: QUERIER
|   DNS_Domain_Name: HTB.LOCAL
|   DNS_Computer_Name: QUERIER.HTB.LOCAL
|   DNS_Tree_Name: HTB.LOCAL
|_  Product_Version: 10.0.17763
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Issuer: commonName=SSL_Self_Signed_Fallback
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2021-08-17T09:10:55
| Not valid after:  2051-08-17T09:10:55
| MD5:   680d 2a6f 7c4b 3a18 52e1 01ff 90f9 8ff6
| SHA-1: 9db5 39c4 63d4 2a29 22e6 a417 044e 8981 78d1 0753
| -----BEGIN CERTIFICATE-----
| MIIDADCCAeigAwIBAgIQPwrl+deMzJVJyGqIeQZVwjANBgkqhkiG9w0BAQsFADA7
| MTkwNwYDVQQDHjAAUwBTAEwAXwBTAGUAbABmAF8AUwBpAGcAbgBlAGQAXwBGAGEA
| bABsAGIAYQBjAGswIBcNMjEwODE3MDkxMDU1WhgPMjA1MTA4MTcwOTEwNTVaMDsx
| OTA3BgNVBAMeMABTAFMATABfAFMAZQBsAGYAXwBTAGkAZwBuAGUAZABfAEYAYQBs
| AGwAYgBhAGMAazCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBANzy921D
| PozU7yNkpheMt6YPS5v5ZfztsTGovN28suBbVP2VIoxvMbqLDuAbnB7rI+/zf3/5
| 55st6vjf5vOuHPLq0vSFJKZ3AK62l/t/jmW7rIChvn9U9R0B+aFBy1JdIJrGVeXL
| Z65O4Y7pXyl+GRcuTjBfhrU8jKpp0kGHTElBK1I/szLuRzC61UJIXCkBm6QfsH0o
| SIKhzsvyRj5UfhWqhFAfcmm07OxpbifdB2isFjEpmF1jJuj0uX/uMZUcFfh9AdhE
| 0+JBxhCSF12rGnYfIqA6eSyrimbFhEPADCqLfeu2yizCXrupxBzEe17prbmgfOCb
| xCYPc9mY3WF57FECAwEAATANBgkqhkiG9w0BAQsFAAOCAQEA1c1ObJOFsUtZNYUB
| 7TXslD3QQZpBDr6YFqBYG87irKJRkN/NjtYGPGN/xmHZCgDfTxwNAieoDFcufxYR
| /Czrl8jRlm53OtIs4d1UTWhZnGUhPraG54eKKbWZSKdGGAxBsJeCWjOnveIRBIl8
| U81nlHUNIUzoHT5PS5bpmSLNvAmDytQ0XDC9I6vSyjs2c0Ln0ponpHXinSvgOFjo
| MOkmwq8UqaJ+RMYhXTeO+HthE81K2vPV7CySsZtaBqe4DdPfv6QFFt4MsOXNfnZl
| Hk4KyJYUv3LYmaBP4ufXgutII2xFsXD5/GtkNblYq1OwLxQmzjWYkKIiBexd9OR+
| CNbFlg==
|_-----END CERTIFICATE-----
|_ssl-date: 2021-08-17T09:26:57+00:00; -1s from scanner time.
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
47001/tcp open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 0s, deviation: 0s, median: -1s
| ms-sql-info: 
|   10.10.10.125:1433: 
|     Version: 
|       name: Microsoft SQL Server 2017 RTM
|       number: 14.00.1000.00
|       Product: Microsoft SQL Server 2017
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 10624/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 55923/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 53986/udp): CLEAN (Timeout)
|   Check 4 (port 40571/udp): CLEAN (Failed to receive data)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-08-17T09:26:54
|_  start_date: N/A

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Aug 17 12:26:58 2021 -- 1 IP address (1 host up) scanned in 132.33 seconds
```