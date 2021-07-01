# 05 - Nmap



# No tcp ports are open
```sql
# Nmap 7.91 scan initiated Thu Jul  1 11:09:22 2021 as: nmap -sC -sV -oA nmap/conceal -T5 10.10.10.116
Nmap scan report for 10.10.10.116
Host is up (0.066s latency).
All 1000 scanned ports on 10.10.10.116 are filtered

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Jul  1 11:10:25 2021 -- 1 IP address (1 host up) scanned in 62.82 seconds
```


```sql
# Nmap 7.91 scan initiated Thu Jul  1 11:24:51 2021 as: nmap -p- -sU -oA nmap/udp 10.10.10.116
Nmap scan report for 10.10.10.116
Host is up (0.067s latency).
Not shown: 65534 open|filtered ports
PORT    STATE SERVICE
500/udp open  isakmp

# Nmap done at Thu Jul  1 12:14:30 2021 -- 1 IP address (1 host up) scanned in 2979.14 seconds
```



