# 05 - Nmap


```sql
# Nmap 7.91 scan initiated Wed Jun  9 11:12:16 2021 as: nmap -sC -sV -p- -oN nmap/jerry 10.10.10.95
Nmap scan report for 10.10.10.95
Host is up (0.067s latency).
Not shown: 65534 filtered ports
PORT     STATE SERVICE VERSION
8080/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
|_http-favicon: Apache Tomcat
|_http-open-proxy: Proxy might be redirecting requests
|_http-server-header: Apache-Coyote/1.1
|_http-title: Apache Tomcat/7.0.88

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Jun  9 11:14:52 2021 -- 1 IP address (1 host up) scanned in 156.45 seconds
```