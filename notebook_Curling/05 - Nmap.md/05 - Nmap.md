# 05 - Nmap


```sql
# Nmap 7.91 scan initiated Mon Aug 30 15:31:35 2021 as: nmap -sC -sV -p- -oA nmap/curling -vvv 10.10.10.150
Nmap scan report for 10.10.10.150
Host is up, received echo-reply ttl 63 (0.12s latency).
Scanned at 2021-08-30 15:31:35 +03 for 83s
Not shown: 65533 closed ports
Reason: 65533 resets
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 7.6p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8a:d1:69:b4:90:20:3e:a7:b6:54:01:eb:68:30:3a:ca (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDGsat32aGJHTbu0gQU9FYIMlMqF/uiytTZ6lsW+EIodvlPp6Cu5VHfs2iEFd5nfn0s+97qTfJ258lf7Gk3rHrULvCrUif2wThIeW3m4fS5j6O2ZPjv0Gl5g02TItSklwQmjJfyH0KR5b1D9bGCXQV3Gm585DD8wZrOpTxDjGCnmByYoHitfG6sa1LC7Sckb8g9Km40fvfKPPWMHgzUhXC3g3wXyjXXeByZvhjbAAuOv7MKda6MjeNUH71hkiQRkTwZ8qqY9fbDDnSKOHdkC2Scs+8tcpz8AIekc/hmDSn+QKbs+3iV0FLoW9TOPmT8xz45etnqW6DhhlcrO7aFju33
|   256 9f:0b:c2:b2:0b:ad:8f:a1:4e:0b:f6:33:79:ef:fb:43 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBN2TI0Uv8Dr/6h+pEZ34kyKx7H6tD1gC/FB4q19PO4klA767pC7YVB3NTdEs2TGI+8XAevVqHiQv/8ZniMwG9IU=
|   256 c1:2a:35:44:30:0c:5b:56:6a:3f:a5:cc:64:66:d9:a9 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILhmU6S36IrO41biIUZrXnzMGw3OZmLLHS/DxqKLPkVU
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.29 ((Ubuntu))
|_http-favicon: Unknown favicon MD5: 1194D7D32448E1F90741A97B42AF91FA
|_http-generator: Joomla! - Open Source Content Management
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Home
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Aug 30 15:32:58 2021 -- 1 IP address (1 host up) scanned in 83.35 seconds

```