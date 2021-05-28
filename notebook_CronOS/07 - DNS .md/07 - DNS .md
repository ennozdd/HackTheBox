# 07 - DNS 

# Reverse DNS query

This box has a dns service running, instead of bruteforcing host header on the website we can perform a reverse dns lookup.
```bash
┌──(kali㉿kali)-[10.10.14.9/23]-[~/htb/cronos]
└─$ nslookup 
> server 10.10.10.13
Default server: 10.10.10.13
Address: 10.10.10.13#53
> 10.10.10.13
13.10.10.10.in-addr.arpa        name = ns1.cronos.htb.
```

cronos.htb turns out to be the domain name for this box.