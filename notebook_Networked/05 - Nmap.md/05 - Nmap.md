# 05 - Nmap

```sql
# Nmap 7.91 scan initiated Sat Jul 10 09:47:39 2021 as: nmap -sC -sV -p- -oA nmap/networked -vvv 10.10.10.146
Nmap scan report for 10.10.10.146
Host is up, received echo-reply ttl 63 (0.083s latency).
Scanned at 2021-07-10 09:47:39 BST for 187s
Not shown: 65532 filtered ports
Reason: 65349 no-responses and 183 host-prohibiteds
PORT    STATE  SERVICE REASON         VERSION
22/tcp  open   ssh     syn-ack ttl 63 OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 22:75:d7:a7:4f:81:a7:af:52:66:e5:27:44:b1:01:5b (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDFgr+LYQ5zL9JWnZmjxP7FT1134sJla89HBT+qnqNvJQRHwO7IqPSa5tEWGZYtzQ2BehsEqb/PisrRHlTeatK0X8qrS3tuz+l1nOj3X/wdcgnFXBrhwpRB2spULt2YqRM49aEbm7bRf2pctxuvgeym/pwCghb6nSbdsaCIsoE+X7QwbG0j6ZfoNIJzQkTQY7O+n1tPP8mlwPOShZJP7+NWVf/kiHsgZqVx6xroCp/NYbQTvLWt6VF/V+iZ3tiT7E1JJxJqQ05wiqsnjnFaZPYP+ptTqorUKP4AenZnf9Wan7VrrzVNZGnFlczj/BsxXOYaRe4Q8VK4PwiDbcwliOBd
|   256 2d:63:28:fc:a2:99:c7:d4:35:b9:45:9a:4b:38:f9:c8 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBAsf1XXvL55L6U7NrCo3XSBTr+zCnnQ+GorAMgUugr3ihPkA+4Tw2LmpBr1syz7Z6PkNyQw6NzC3KwSUy1BOGw8=
|   256 73:cd:a0:5b:84:10:7d:a7:1c:7c:61:1d:f5:54:cf:c4 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILMrhnJBfdb0fWQsWVfynAxcQ8+SNlL38vl8VJaaqPTL
80/tcp  open   http    syn-ack ttl 63 Apache httpd 2.4.6 ((CentOS) PHP/5.4.16)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.6 (CentOS) PHP/5.4.16
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
443/tcp closed https   reset ttl 63

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Jul 10 09:50:46 2021 -- 1 IP address (1 host up) scanned in 186.90 seconds
```