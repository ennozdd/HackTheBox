# 05 - Nmap

```sql
# Nmap 7.91 scan initiated Thu Jul  8 16:50:56 2021 as: nmap -sC -sV -p- -oA nmap/lightweight -vvv 10.10.10.119
Nmap scan report for 10.10.10.119
Host is up, received echo-reply ttl 63 (0.081s latency).
Scanned at 2021-07-08 16:50:57 BST for 220s
Not shown: 65532 filtered ports
Reason: 65324 no-responses and 208 host-prohibiteds
PORT    STATE SERVICE REASON         VERSION
22/tcp  open  ssh     syn-ack ttl 63 OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 19:97:59:9a:15:fd:d2:ac:bd:84:73:c4:29:e9:2b:73 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDDf7K92wk79uG+iF3K0XaLWtJBrMKM/PfpE01tmpOSxwdhbiXQZ1ggfXFOfjSrkNqO/W3apn2SH1IO3jRCUGmEfXUzmTlX7FKDETKKFJuSZFwdphEqxoX/wCZ+NQhBX9bMT817GjQTNPEmkQsuWUD7PcVBYhRSKohP0jbAc464VKbSeiQt6q1I71CxzUtqMnL7pOREvF41+0K0BNtQUJVKxq5Aq0g67Ba8b0UEecOwgS8O4rZeKrfuYHMXnl6n32XrjqliowOSaZl/iYOu3dgkooIEDFDiaEapOW7J71/Ag/96NWzUf1U91QxCIA2GNtAhXT+Bn+ncbFtWxGdh6enL
|   256 88:58:a1:cf:38:cd:2e:15:1d:2c:7f:72:06:a3:57:67 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBJ2F5pumDKrMj6rP99uQehJ2kGbw7z54Ydq7uuZ8FgoTw7wJ44SSytCh1jkrQay1jRg0+4Izw0cqUeW93J5kDCc=
|   256 31:6c:c1:eb:3b:28:0f:ad:d5:79:72:8f:f5:b5:49:db (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIGwL0BBmHKyKlj3sRMsytml1etD3lMtofGbdxD8aAh1T
80/tcp  open  http    syn-ack ttl 63 Apache httpd 2.4.6 ((CentOS) OpenSSL/1.0.2k-fips mod_fcgid/2.3.9 PHP/5.4.16)
| http-methods: 
|_  Supported Methods: GET HEAD POST
|_http-title: Lightweight slider evaluation page - slendr
389/tcp open  ldap    syn-ack ttl 63 OpenLDAP 2.2.X - 2.3.X
| ssl-cert: Subject: commonName=lightweight.htb
| Subject Alternative Name: DNS:lightweight.htb, DNS:localhost, DNS:localhost.localdomain
| Issuer: commonName=lightweight.htb
| Public Key type: rsa
| Public Key bits: 1024
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2018-06-09T13:32:51
| Not valid after:  2019-06-09T13:32:51
| MD5:   0e61 1374 e591 83bd fd4a ee1a f448 547c
| SHA-1: 8e10 be17 d435 e99d 3f93 9f40 c5d9 433c 47dd 532f
| -----BEGIN CERTIFICATE-----
| MIIB7jCCAVegAwIBAgIFAK3GsbIwDQYJKoZIhvcNAQELBQAwGjEYMBYGA1UEAxMP
| bGlnaHR3ZWlnaHQuaHRiMB4XDTE4MDYwOTEzMzI1MVoXDTE5MDYwOTEzMzI1MVow
| GjEYMBYGA1UEAxMPbGlnaHR3ZWlnaHQuaHRiMIGfMA0GCSqGSIb3DQEBAQUAA4GN
| ADCBiQKBgQCxvnGKmYo2hrfZIWhsg4xxexD5taBmlczGdn8RSN3/X4ByGY17Uk1J
| 8JfYiCVYaD78Hi1QjZVKqpTZQdrU5KC1JqREWvBH/dw+Oat1Q0hFQs1Kuuk7oCAy
| hxYBsqbdqG1j++xAxDRNVJE4rzAS84MkMuM19RcxXdftJKmYaCBoQwIDAQABo0Aw
| PjA8BgNVHREENTAzgg9saWdodHdlaWdodC5odGKCCWxvY2FsaG9zdIIVbG9jYWxo
| b3N0LmxvY2FsZG9tYWluMA0GCSqGSIb3DQEBCwUAA4GBAHcHUNMIiasynONFZpFm
| ehiY2mIbB8YpPfFu5aCyMr0Ws/Zwb2eBkuSW5NDY2J2qqPwlUJcy+pqzYpZHE40z
| Q/rvhBc2XglTApQp4wxFEGRLAoxLmerI/OluxwpYb+J0oKJcf/7gWA+JNRSNP8bY
| cCCEDJ6JnmORKAK04GxKbB+T
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Jul  8 16:54:37 2021 -- 1 IP address (1 host up) scanned in 220.37 seconds

```