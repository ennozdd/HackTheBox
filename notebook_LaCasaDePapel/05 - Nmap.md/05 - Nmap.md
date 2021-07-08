# 05 - Nmap


```sql
# Nmap 7.91 scan initiated Mon Jul  5 14:02:10 2021 as: nmap -sC -sV -p- -oA nmap/lacasadepapel -vvv 10.10.10.131
Increasing send delay for 10.10.10.131 from 0 to 5 due to 193 out of 642 dropped probes since last increase.
Increasing send delay for 10.10.10.131 from 5 to 10 due to 36 out of 118 dropped probes since last increase.
Increasing send delay for 10.10.10.131 from 10 to 20 due to 22 out of 73 dropped probes since last increase.
Nmap scan report for 10.10.10.131
Host is up, received echo-reply ttl 63 (0.14s latency).
Scanned at 2021-07-05 14:02:10 BST for 2399s
Not shown: 65530 closed ports
Reason: 65530 resets
PORT     STATE    SERVICE  REASON              VERSION
21/tcp   open     ftp      syn-ack ttl 63      vsftpd 2.3.4
22/tcp   open     ssh      syn-ack ttl 63      OpenSSH 7.9 (protocol 2.0)
| ssh-hostkey: 
|   2048 03:e1:c2:c9:79:1c:a6:6b:51:34:8d:7a:c3:c7:c8:50 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDNzmarvyIINA+hjsLo2xYn1PUyzuTflhtXQs8S1Z56FzbdzXs6FiwhoRGn63XuGCHqCfEzHmh1cg4HGLfGAMwe+AsdJ8hLd/ISNRECH8yvM+9k78Aio3pe+lYbiWSQWyJrQdeqJXyDJFSd6BR3Cr6/rwSvE7N3eWeQvxS+fsg5HOER6n8SOnXvqpWYUo+XmZxGzmluNfsqoJ6doJCyW3X4sTImTlpmRmee6iseo9neZO18aHsARxlkHCqUhp1SBzIiik3DurtH1tgrn8ntfNiK3q0FZJmh9qzu0P/L50j8bzlJdvAsLuqbYmVZhqFs0JfBVdyVTFMn4O0J+IqRrXAF
|   256 41:e4:95:a3:39:0b:25:f9:da:de:be:6a:dc:59:48:6d (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBNli8Xx10a0s+zrkT1eVfM1kRaAQaK+a/mxYxhPxpK0094QFQBcVrvrXb3+j4M8l2G/C9CtQRWVXpX8ajWhYRik=
|   256 30:0b:c6:66:2b:8f:5e:4f:26:28:75:0e:f5:b1:71:e4 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIB2uNaKo2PK5cMci4E7dNWQ6ipiEzG3cWUR56qqMZqYR
80/tcp   open     http     syn-ack ttl 63      Node.js (Express middleware)
|_http-favicon: Unknown favicon MD5: 621D76BDE56526A10B529BF2BC0776CA
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: La Casa De Papel
443/tcp  open     ssl/http syn-ack ttl 63      Node.js Express framework
| http-auth: 
| HTTP/1.1 401 Unauthorized\x0D
|_  Server returned status 401 but no WWW-Authenticate header.
| http-methods: 
|_  Supported Methods: GET OPTIONS| ssl-cert: Subject: commonName=lacasadepapel.htb/organizationName=La Casa De Papel
| Issuer: commonName=lacasadepapel.htb/organizationName=La Casa De Papel
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2019-01-27T08:35:30
| Not valid after:  2029-01-24T08:35:30
| MD5:   6ea4 933a a347 ce50 8c40 5f9b 1ea8 8e9a
| SHA-1: 8c47 7f3e 53d8 e76b 4cdf ecca adb6 0551 b1b6 38d4
| -----BEGIN CERTIFICATE-----
| MIIC6jCCAdICCQDISiE8M6B29jANBgkqhkiG9w0BAQsFADA3MRowGAYDVQQDDBFs
| YWNhc2FkZXBhcGVsLmh0YjEZMBcGA1UECgwQTGEgQ2FzYSBEZSBQYXBlbDAeFw0x
| OTAxMjcwODM1MzBaFw0yOTAxMjQwODM1MzBaMDcxGjAYBgNVBAMMEWxhY2FzYWRl
| cGFwZWwuaHRiMRkwFwYDVQQKDBBMYSBDYXNhIERlIFBhcGVsMIIBIjANBgkqhkiG
| 9w0BAQEFAAOCAQ8AMIIBCgKCAQEAz3M6VN7OD5sHW+zCbIv/5vJpuaxJF3A5q2rV
| QJNqU1sFsbnaPxRbFgAtc8hVeMNii2nCFO8PGGs9P9pvoy8e8DR9ksBQYyXqOZZ8
| /rsdxwfjYVgv+a3UbJNO4e9Sd3b8GL+4XIzzSi3EZbl7dlsOhl4+KB4cM4hNhE5B
| 4K8UKe4wfKS/ekgyCRTRENVqqd3izZzz232yyzFvDGEOFJVzmhlHVypqsfS9rKUV
| ESPHczaEQld3kupVrt/mBqwuKe99sluQzORqO1xMqbNgb55ZD66vQBSkN2PwBeiR
| PBRNXfnWla3Gkabukpu9xR9o+l7ut13PXdQ/fPflLDwnu5wMZwIDAQABMA0GCSqG
| SIb3DQEBCwUAA4IBAQCuo8yzORz4pby9tF1CK/4cZKDYcGT/wpa1v6lmD5CPuS+C
| hXXBjK0gPRAPhpF95DO7ilyJbfIc2xIRh1cgX6L0ui/SyxaKHgmEE8ewQea/eKu6
| vmgh3JkChYqvVwk7HRWaSaFzOiWMKUU8mB/7L95+mNU7DVVUYB9vaPSqxqfX6ywx
| BoJEm7yf7QlJTH3FSzfew1pgMyPxx0cAb5ctjQTLbUj1rcE9PgcSki/j9WyJltkI
| EqSngyuJEu3qYGoM0O5gtX13jszgJP+dA3vZ1wqFjKlWs2l89pb/hwRR2raqDwli
| MgnURkjwvR1kalXCvx9cST6nCkxF2TxlmRpyNXy4
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
| tls-nextprotoneg: 
|   http/1.1
|_  http/1.0
6200/tcp filtered lm-x     port-unreach ttl 63
Service Info: OS: Unix

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Jul  5 14:42:09 2021 -- 1 IP address (1 host up) scanned in 2398.64 seconds
```