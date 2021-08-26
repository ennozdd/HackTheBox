# 05 - Nmap



```sql
# Nmap 7.91 scan initiated Thu Aug 26 11:18:55 2021 as: nmap -sC -sV -p- -oA nmap/haystack -vvv 10.10.10.115
Nmap scan report for 10.10.10.115
Host is up, received echo-reply ttl 63 (0.081s latency).
Scanned at 2021-08-26 11:18:55 +03 for 421s
Not shown: 65532 filtered ports
Reason: 65120 no-responses and 412 host-prohibiteds
PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 63 OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 2a:8d:e2:92:8b:14:b6:3f:e4:2f:3a:47:43:23:8b:2b (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCk83gZJYhPRnV/Iuqd18UJy4nedzzs4V/uA5R+YrGC6fAgaZEDH7rEs3M1Fdbikvl6r50GCzSI0Svwx9oACM/1TmEzJ+HB5wfr4wD9JGwUCKxxiS5KJzIDMUKY0tHDqAZXvLJv1Xy7sDu/lDHkvwXTm4sXq400nqYP03i1kefaAcLFEFoYfnJo4fANNZre0in8332B6Nfe+FEiGXT+nMR2qhtInqOE3wB5HmNJiuCiP4iqUzSUhgF8ppRFTVF/n2z5zNb7Q2Rz1kNVBgKACF5tCT4p1gKCT/yHJaBUc9CwYcbN7MpwEVfddCOzvq+TkcZs54XoIz7OjDE2jUsULcnz
|   256 e7:5a:3a:97:8e:8e:72:87:69:a3:0d:d1:00:bc:1f:09 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBGN/Ph011yq25jPz8RztnAPINzUswaLL6R8u8K0gIWJ0cdILzG1LijJnSPYBdjfIXhMzj/a1CM5O/4uf5lq6bXM=
|   256 01:d2:59:b2:66:0a:97:49:20:5f:1c:84:eb:81:ed:95 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIPQ8doXk4d9F3phggcBReCM3Or+FvRE7rjLCw1W6LTjX
80/tcp   open  http    syn-ack ttl 63 nginx 1.12.2
| http-methods: 
|_  Supported Methods: GET HEAD
|_http-server-header: nginx/1.12.2
|_http-title: Site doesn't have a title (text/html).
9200/tcp open  http    syn-ack ttl 63 nginx 1.12.2
|_http-favicon: Unknown favicon MD5: 6177BFB75B498E0BB356223ED76FFE43
| http-methods: 
|   Supported Methods: HEAD DELETE GET OPTIONS
|_  Potentially risky methods: DELETE
|_http-server-header: nginx/1.12.2
|_http-title: Site doesn't have a title (application/json; charset=UTF-8).

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Aug 26 11:25:56 2021 -- 1 IP address (1 host up) scanned in 421.67 seconds
```