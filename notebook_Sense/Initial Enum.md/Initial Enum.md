# Initial Enum

```sql
# Nmap 7.91 scan initiated Thu May 13 11:36:04 2021 as: nmap -sC -sV -p- -oA nmap/sense 10.10.10.60
Nmap scan report for 10.10.10.60
Host is up (0.066s latency).
Not shown: 65533 filtered ports
PORT    STATE SERVICE    VERSION
80/tcp  open  http       lighttpd 1.4.35
|_http-server-header: lighttpd/1.4.35
|_http-title: Did not follow redirect to https://10.10.10.60/
443/tcp open  ssl/https?
| ssl-cert: Subject: commonName=Common Name (eg, YOUR name)/organizationName=CompanyName/stateOrProvinceName=Somewhere/countryName=US
| Not valid before: 2017-10-14T19:21:35
|_Not valid after:  2023-04-06T19:21:35
|_ssl-date: TLS randomness does not represent time

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu May 13 11:38:02 2021 -- 1 IP address (1 host up) scanned in 118.18 seconds
```