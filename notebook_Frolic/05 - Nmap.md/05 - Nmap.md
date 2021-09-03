# 05 - Nmap

```sql
# Nmap 7.91 scan initiated Tue Aug 31 17:25:01 2021 as: nmap -sC -sV -p- -oA nmap/frolic -vvv 10.10.10.111
Nmap scan report for 10.10.10.111
Host is up, received echo-reply ttl 63 (0.091s latency).
Scanned at 2021-08-31 17:25:02 +03 for 106s
Not shown: 65530 closed ports
Reason: 65530 resets
PORT     STATE SERVICE     REASON         VERSION
22/tcp   open  ssh         syn-ack ttl 63 OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 87:7b:91:2a:0f:11:b6:57:1e:cb:9f:77:cf:35:e2:21 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC3HUqxhCShF9I6uBmGCX6yXz56Iibv7WW2fBKsKA9yVqmoupPdDKac1U3/PIioRNHkPC03r5ZXsqfALwjIWEits7toO4K+9VSFU6d0qhmpUZW3WwiyxdcPxmTQLpU8InXZpMOwjpGJTTwqxsMIxNdPk0FP/MtqEzQI45MOr7IQOGcEAsmcJ1Cy3aRDAnp77NBWYA316l7Xb8WA/aWoHEyS/6Qf3XzeARf0yZ6YwYg4TTsaeQtfRr4HWZBDs7fLrrWUzN0ivb9izy9YgqrOJ5ZKQI4A1yn0CxZNsiweIT8gopM1KrfinPGiKbGbSNVvTX2dHYyISh6Y2bp1D5vum6SH
|   256 b7:9b:06:dd:c2:5e:28:44:78:41:1e:67:7d:1e:b7:62 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBDSjEcHeA/VoBi4PaoyxwM1Rx1vpoQofoJPYTxBuQLXRujf3gqn491cWpd2CDh2mF/3w2kEGsrWRwqD4LZmz+Sk=
|   256 21:cf:16:6d:82:a4:30:c3:c6:9c:d7:38:ba:b5:02:b0 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINVT+d0lX5zwXTOY4h4+MfU6kt/q3EmGVWIXnMsomQq5
139/tcp  open  netbios-ssn syn-ack ttl 63 Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn syn-ack ttl 63 Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
1880/tcp open  http        syn-ack ttl 63 Node.js (Express middleware)
|_http-favicon: Unknown favicon MD5: 818DD6AFD0D0F9433B21774F89665EEA
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Node-RED
9999/tcp open  http        syn-ack ttl 63 nginx 1.10.3 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD
|_http-server-header: nginx/1.10.3 (Ubuntu)
|_http-title: Welcome to nginx!
Service Info: Host: FROLIC; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: -1h50m00s, deviation: 3h10m31s, median: -1s
| nbstat: NetBIOS name: FROLIC, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| Names:
|   FROLIC<00>           Flags: <unique><active>
|   FROLIC<03>           Flags: <unique><active>
|   FROLIC<20>           Flags: <unique><active>
|   \x01\x02__MSBROWSE__\x02<01>  Flags: <group><active>
|   WORKGROUP<00>        Flags: <group><active>
|   WORKGROUP<1d>        Flags: <unique><active>
|   WORKGROUP<1e>        Flags: <group><active>
| Statistics:
|   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
|   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
|_  00 00 00 00 00 00 00 00 00 00 00 00 00 00
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 56356/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 50509/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 36186/udp): CLEAN (Failed to receive data)
|   Check 4 (port 32714/udp): CLEAN (Failed to receive data)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: frolic
|   NetBIOS computer name: FROLIC\x00
|   Domain name: \x00
|   FQDN: frolic
|_  System time: 2021-08-31T19:56:45+05:30
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-08-31T14:26:45
|_  start_date: N/A

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Aug 31 17:26:48 2021 -- 1 IP address (1 host up) scanned in 106.67 seconds

```


Yes, this is a linux box. It is hosting SMB, which is unusual for a linux box. Other than that we have other ports that we can enumerate and fortunately, they are http, the protocol we are most familiar with.
According to nmap, smb guest login enabled but there is no read/write access on any of the shares. Credentials are needed  if we want to get something from smb.