# 15 - SNMP


```
snmp-check v1.9 - SNMP enumerator
Copyright (c) 2005-2015 by Matteo Cantoni (www.nothink.org)

[+] Try to connect to 10.10.10.20:161 using SNMPv1 and community 'public'

[*] System information:

  Host IP address               : 10.10.10.20
  Hostname                      : Sneaky
  Description                   : Linux Sneaky 4.4.0-75-generic #96~14.04.1-Ubuntu SMP Thu Apr 20 11:06:56 UTC 2017 i686
  Contact                       : root
  Location                      : Unknown
  Uptime snmp                   : 01:52:40.58
  Uptime system                 : 01:52:35.80
  System date                   : 2021-7-16 20:57:01.0


[*] Network interfaces:

  Interface                     : [ up ] lo
  Id                            : 1
  Mac Address                   : :::::
  Type                          : softwareLoopback
  Speed                         : 10 Mbps
  MTU                           : 65536
  In octets                     : 132608
  Out octets                    : 132608

  Interface                     : [ up ] eth0
  Id                            : 2
  Mac Address                   : 00:50:56:b9:ef:4e
  Type                          : ethernet-csmacd
  Speed                         : 4294 Mbps
  MTU                           : 1500
  In octets                     : 307485895
  Out octets                    : 872254578
```

IPv6 address is not shown here

# [snmpwalk](http://www.net-snmp.org/download.html)
snmp-mibs-downloader package is also needed for prettier output.
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/sneaky]
└──╼ $ sudo apt  install snmp-mibs-downloader
```


# load mibs for snmpwalk
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/sneaky]
└──╼ $ cat /etc/snmp/snmp.conf 
# As the snmp packages come without MIB files due to license reasons, loading
# of MIBs is disabled by default. If you added the MIBs you can reenable
# loading them by commenting out the following line.
# mibs :

# If you want to globally change where snmp libraries, commands and daemons
# look for MIBS, change the line below. Note you can set this for individual
# tools with the -M option or MIBDIRS environment variable.
#
# mibdirs /usr/share/snmp/mibs:/usr/share/snmp/mibs/iana:/usr/share/snmp/mibs/ietf
```

# IPv6
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/sneaky]
└──╼ $ snmpwalk -c public -v2c 10.10.10.20   | grep -i ipv6 
IP-FORWARD-MIB::inetCidrRouteIfIndex.ipv6."00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00".0.3.0.0.4.ipv6."fe:80:00:00:00:00:00:00:02:50:56:ff:fe:b9:c0:c3" = INTEGER: 2
IP-FORWARD-MIB::inetCidrRouteIfIndex.ipv6."00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:01".128.3.0.0.6.ipv6."00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00" = INTEGER: 1
IP-FORWARD-MIB::inetCidrRouteIfIndex.ipv6."de:ad:be:ef:00:00:00:00:02:50:56:ff:fe:b9:ef:4e".128.3.0.0.7.ipv6."00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00" = INTEGER: 1
IP-FORWARD-MIB::inetCidrRouteIfIndex.ipv6."fe:80:00:00:00:00:00:00:00:00:00:00:00:00:00:00".64.3.0.0.3.ipv6."00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00" = INTEGER: 2
IP-FORWARD-MIB::inetCidrRouteIfIndex.ipv6."fe:80:00:00:00:00:00:00:02:50:56:ff:fe:b9:ef:4e".128.3.0.0.8.ipv6."00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00" = INTEGER: 1
```


# ICMPv6
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/sneaky]
└──╼ $ ping6 -I tun0 dead:beef:0000:0000:0250:56ff:feb9:ef4e
PING dead:beef:0000:0000:0250:56ff:feb9:ef4e(dead:beef::250:56ff:feb9:ef4e) from dead:beef:2::1010 tun0: 56 data bytes
64 bytes from dead:beef::250:56ff:feb9:ef4e: icmp_seq=1 ttl=63 time=63.9 ms
64 bytes from dead:beef::250:56ff:feb9:ef4e: icmp_seq=2 ttl=63 time=64.4 ms
64 bytes from dead:beef::250:56ff:feb9:ef4e: icmp_seq=3 ttl=63 time=64.3 ms
64 bytes from dead:beef::250:56ff:feb9:ef4e: icmp_seq=4 ttl=63 time=64.2 ms
```


# Nmap 
```
┌─[user@parrot]─[10.10.14.18]─[~/htb/sneaky]
└──╼ $ nmap -p 22 -6 dead:beef:0000:0000:0250:56ff:feb9:ef4e
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-17 18:03 +03
Nmap scan report for dead:beef::250:56ff:feb9:ef4e
Host is up (0.068s latency).

PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 1 IP address (1 host up) scanned in 0.47 seconds
```

SSH is open for  IPv6  addresses


# SSH 
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/sneaky]
└──╼ $ ssh   -l thrasivoulos  dead:beef:0000:0000:0250:56ff:feb9:ef4e -i thrasivoulos.key 
Welcome to Ubuntu 14.04.5 LTS (GNU/Linux 4.4.0-75-generic i686)

 * Documentation:  https://help.ubuntu.com/

  System information as of Sat Jul 17 18:22:06 EEST 2021

  System load:  0.01               Processes:           162
  Usage of /:   10.7% of 18.58GB   Users logged in:     0
  Memory usage: 34%                IP address for eth0: 10.10.10.20
  Swap usage:   0%

  Graph this data and manage this system at:
    https://landscape.canonical.com/

Your Hardware Enablement Stack (HWE) is supported until April 2019.
Last login: Sat Jul 17 18:22:06 2021 from dead:beef:2::1010
thrasivoulos@Sneaky:~$ 
```
