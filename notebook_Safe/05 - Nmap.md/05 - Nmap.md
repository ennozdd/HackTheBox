# 05 - Nmap


```sql
# Nmap 7.91 scan initiated Mon Jul 12 10:38:16 2021 as: nmap -sC -sV -p- -oA nmap/safe -vvv 10.10.10.147
Nmap scan report for 10.10.10.147
Host is up, received echo-reply ttl 63 (0.071s latency).
Scanned at 2021-07-12 10:38:16 BST for 166s
Not shown: 65532 closed ports
Reason: 65532 resets
PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 63 OpenSSH 7.4p1 Debian 10+deb9u6 (protocol 2.0)
| ssh-hostkey: 
|   2048 6d:7c:81:3d:6a:3d:f9:5f:2e:1f:6a:97:e5:00:ba:de (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC1lhlptw4YE96mogUlBKcqkeUXEOiCLbQxwjfzb4Zv7ddGBtF3jBi1mitjd+njlQQn9KqVXjPjtoEp17iSyI851O++s5SiSt1bIALdd4DA+n65dGZUvotBah+rTCrPa8yUyQ9NaXO1e2ALHZ+qWJJDBYULqTYrqObF1fErk+uaJ2EInSm4O3E4a1rDJP9M6OFInq9er3dVVXzR7pyIyLLiGOnmwrm+XX9/YZ3i9R+S4yb4OexUzLE6s52ZQMPaznExnAnA7EXFojw1+VT5sncZ4hiqBvaYXFHLRZTytiKYO4Bf/Ntl1+IOOQjyvpSnxVy+Riew/AZXMm3qwl/MrNdX
|   256 99:7e:1e:22:76:72:da:3c:c9:61:7d:74:d7:80:33:d2 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBCBjZCYZ/SIu/q2bMhVAICKM1a09kOxqXxGZ/Skm0OnzqhoF3Tj2+F6OfYr7yFoF8/SzWiKAOdmyYafg/mTJVT8=
|   256 6a:6b:c3:8e:4b:28:f7:60:85:b1:62:ff:54:bc:d8:d6 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINspYs2G7atyE7B4AbsflH8zPxqXWDZv89V1FD9q5ZtB
80/tcp   open  http    syn-ack ttl 63 Apache httpd 2.4.25 ((Debian))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.25 (Debian)
|_http-title: Apache2 Debian Default Page: It works
1337/tcp open  waste?  syn-ack ttl 63
| fingerprint-strings: 
|   DNSStatusRequestTCP: 
|     05:47:12 up 11 min, 0 users, load average: 0.00, 0.00, 0.00
|   DNSVersionBindReqTCP: 
|     05:47:07 up 11 min, 0 users, load average: 0.00, 0.00, 0.00
|   GenericLines: 
|     05:46:55 up 11 min, 0 users, load average: 0.00, 0.00, 0.00
|     What do you want me to echo back?
|   GetRequest: 
|     05:47:01 up 11 min, 0 users, load average: 0.00, 0.00, 0.00
|     What do you want me to echo back? GET / HTTP/1.0
|   HTTPOptions: 
|     05:47:01 up 11 min, 0 users, load average: 0.00, 0.00, 0.00
|     What do you want me to echo back? OPTIONS / HTTP/1.0
|   Help: 
|     05:47:17 up 11 min, 0 users, load average: 0.00, 0.00, 0.00
|     What do you want me to echo back? HELP
|   NULL: 
|     05:46:55 up 11 min, 0 users, load average: 0.00, 0.00, 0.00
|   RPCCheck: 
|     05:47:01 up 11 min, 0 users, load average: 0.00, 0.00, 0.00
|   RTSPRequest: 
|     05:47:01 up 11 min, 0 users, load average: 0.00, 0.00, 0.00
|     What do you want me to echo back? OPTIONS / RTSP/1.0
|   SSLSessionReq, TLSSessionReq, TerminalServerCookie: 
|     05:47:17 up 11 min, 0 users, load average: 0.00, 0.00, 0.00
|_    What do you want me to echo back?
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port1337-TCP:V=7.91%I=7%D=7/12%Time=60EC0DD8%P=x86_64-pc-linux-gnu%r(NU
SF:LL,3F,"\x2005:46:55\x20up\x2011\x20min,\x20\x200\x20users,\x20\x20load\
SF:x20average:\x200\.00,\x200\.00,\x200\.00\n")%r(GenericLines,64,"\x2005:
SF:46:55\x20up\x2011\x20min,\x20\x200\x20users,\x20\x20load\x20average:\x2
SF:00\.00,\x200\.00,\x200\.00\n\nWhat\x20do\x20you\x20want\x20me\x20to\x20
SF:echo\x20back\?\x20\r\n")%r(GetRequest,72,"\x2005:47:01\x20up\x2011\x20m
SF:in,\x20\x200\x20users,\x20\x20load\x20average:\x200\.00,\x200\.00,\x200
SF:\.00\n\nWhat\x20do\x20you\x20want\x20me\x20to\x20echo\x20back\?\x20GET\
SF:x20/\x20HTTP/1\.0\r\n")%r(HTTPOptions,76,"\x2005:47:01\x20up\x2011\x20m
SF:in,\x20\x200\x20users,\x20\x20load\x20average:\x200\.00,\x200\.00,\x200
SF:\.00\n\nWhat\x20do\x20you\x20want\x20me\x20to\x20echo\x20back\?\x20OPTI
SF:ONS\x20/\x20HTTP/1\.0\r\n")%r(RTSPRequest,76,"\x2005:47:01\x20up\x2011\
SF:x20min,\x20\x200\x20users,\x20\x20load\x20average:\x200\.00,\x200\.00,\
SF:x200\.00\n\nWhat\x20do\x20you\x20want\x20me\x20to\x20echo\x20back\?\x20
SF:OPTIONS\x20/\x20RTSP/1\.0\r\n")%r(RPCCheck,3F,"\x2005:47:01\x20up\x2011
SF:\x20min,\x20\x200\x20users,\x20\x20load\x20average:\x200\.00,\x200\.00,
SF:\x200\.00\n")%r(DNSVersionBindReqTCP,3F,"\x2005:47:07\x20up\x2011\x20mi
SF:n,\x20\x200\x20users,\x20\x20load\x20average:\x200\.00,\x200\.00,\x200\
SF:.00\n")%r(DNSStatusRequestTCP,3F,"\x2005:47:12\x20up\x2011\x20min,\x20\
SF:x200\x20users,\x20\x20load\x20average:\x200\.00,\x200\.00,\x200\.00\n")
SF:%r(Help,68,"\x2005:47:17\x20up\x2011\x20min,\x20\x200\x20users,\x20\x20
SF:load\x20average:\x200\.00,\x200\.00,\x200\.00\n\nWhat\x20do\x20you\x20w
SF:ant\x20me\x20to\x20echo\x20back\?\x20HELP\r\n")%r(SSLSessionReq,65,"\x2
SF:005:47:17\x20up\x2011\x20min,\x20\x200\x20users,\x20\x20load\x20average
SF::\x200\.00,\x200\.00,\x200\.00\n\nWhat\x20do\x20you\x20want\x20me\x20to
SF:\x20echo\x20back\?\x20\x16\x03\n")%r(TerminalServerCookie,64,"\x2005:47
SF::17\x20up\x2011\x20min,\x20\x200\x20users,\x20\x20load\x20average:\x200
SF:\.00,\x200\.00,\x200\.00\n\nWhat\x20do\x20you\x20want\x20me\x20to\x20ec
SF:ho\x20back\?\x20\x03\n")%r(TLSSessionReq,65,"\x2005:47:17\x20up\x2011\x
SF:20min,\x20\x200\x20users,\x20\x20load\x20average:\x200\.00,\x200\.00,\x
SF:200\.00\n\nWhat\x20do\x20you\x20want\x20me\x20to\x20echo\x20back\?\x20\
SF:x16\x03\n");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Jul 12 10:41:02 2021 -- 1 IP address (1 host up) scanned in 165.79 seconds
```