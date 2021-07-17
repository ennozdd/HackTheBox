# 05 - Nmap


# TCP
```sql
# Nmap 7.91 scan initiated Fri Jul 16 18:58:56 2021 as: nmap -sC -sV -p- -oA nmap/sneaky -vvv 10.10.10.20
Nmap scan report for 10.10.10.20
Host is up, received echo-reply ttl 63 (0.076s latency).
Scanned at 2021-07-16 18:58:57 +03 for 80s
Not shown: 65534 closed ports
Reason: 65534 resets
PORT   STATE SERVICE REASON         VERSION
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.7 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: Under Development!

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Jul 16 19:00:17 2021 -- 1 IP address (1 host up) scanned in 81.61 seconds
```


# UDP

```sql
# Nmap 7.91 scan initiated Fri Jul 16 21:03:55 2021 as: nmap -p 161 -sU -v -oA nmap/udp 10.10.10.20
Nmap scan report for 10.10.10.20
Host is up (0.071s latency).

PORT    STATE         SERVICE
161/udp open|filtered snmp

Read data files from: /usr/bin/../share/nmap
# Nmap done at Fri Jul 16 21:03:56 2021 -- 1 IP address (1 host up) scanned in 1.23 seconds
```