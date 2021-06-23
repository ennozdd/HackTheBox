# 05 - Nmap

```sql
# Nmap 7.91 scan initiated Mon Jun 21 13:07:15 2021 as: nmap -sC -sV -p- -oA nmap/jail -vvv 10.10.10.34
Nmap scan report for 10.10.10.34
Host is up, received echo-reply ttl 63 (0.082s latency).
Scanned at 2021-06-21 13:07:15 BST for 367s
Not shown: 65529 filtered ports
Reason: 65346 no-responses and 183 host-prohibiteds
PORT      STATE SERVICE    REASON         VERSION
22/tcp    open  ssh        syn-ack ttl 63 OpenSSH 6.6.1 (protocol 2.0)
| ssh-hostkey: 
|   2048 cd:ec:19:7c:da:dc:16:e2:a3:9d:42:f3:18:4b:e6:4d (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC10JBZuYCiFDOwkbbeqZLrL1s7wXMbVZxPJOg4cW4gdpi1OvuyiWsJ09dbfCzjnUjNzA/e2RU7+LNygV2XlDPNCltWmuBQX1aBihxmK7iFMRjM12Yeg90h1kKlezc3WOv+M1YREOIKFBW7jbUiwf4z2z+tfi92d3ZN58FgAmysPaLVR/Ct+pd9AyiSJiLCEzVYWN78lQd09D33yl1MY9no85qaWr5lgnZ3YEd7kTtCXFjICiMgir3zCrZCRHHobsMH+FO3RqbOv9AHfe51rtid9UXRojgSMuzfDV19x/PwYNFMuuAhnJVFRCxXClawpILp2YuBTFJsu1juXDcqfJD/
|   256 af:94:9f:2f:21:d0:e0:1d:ae:8e:7f:1d:7b:d7:42:ef (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBDm08eT3joqYGfJK9t2+Bn5vXB5FHMnM7DIFVhXG3Up5XYwgxOnywl8gBGtcWtXqXNUkyqP8dApTHh9wljFH5A0=
|   256 6b:f8:dc:27:4f:1c:89:67:a4:67:c5:ed:07:53:af:97 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJLJbZLS01Zdaxy/HoDmoUF7fBBi3BhS/NW9NShcGaOs
80/tcp    open  http       syn-ack ttl 63 Apache httpd 2.4.6 ((CentOS))
| http-methods: 
|   Supported Methods: POST OPTIONS GET HEAD TRACE
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.6 (CentOS)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
111/tcp   open  rpcbind    syn-ack ttl 63 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100003  3,4         2049/udp   nfs
|   100003  3,4         2049/udp6  nfs
|   100005  1,2,3      20048/tcp   mountd
|   100005  1,2,3      20048/tcp6  mountd
|   100005  1,2,3      20048/udp   mountd
|   100005  1,2,3      20048/udp6  mountd
|   100021  1,3,4      33047/udp6  nlockmgr
|   100021  1,3,4      42119/tcp6  nlockmgr
|   100021  1,3,4      44809/tcp   nlockmgr
|   100021  1,3,4      46337/udp   nlockmgr
|   100024  1          44857/tcp6  status
|   100024  1          49710/udp6  status
|   100024  1          53892/udp   status
|   100024  1          57881/tcp   status
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
2049/tcp  open  nfs_acl    syn-ack ttl 63 3 (RPC #100227)
7411/tcp  open  daqstream? syn-ack ttl 63
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, FourOhFourRequest, GenericLines, GetRequest, HTTPOptions, Help, JavaRMI, Kerberos, LANDesk-RC, LDAPBindReq, LDAPSearchReq, LPDString, NCP, NULL, NotesRPC, RPCCheck, RTSPRequest, SIPOptions, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServer, TerminalServerCookie, WMSRequest, X11Probe, afp, giop, ms-sql-s, oracle-tns: 
|_    OK Ready. Send USER command.
20048/tcp open  mountd     syn-ack ttl 63 1-3 (RPC #100005)
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port7411-TCP:V=7.91%I=7%D=6/21%Time=60D081AC%P=x86_64-pc-linux-gnu%r(NU
SF:LL,1D,"OK\x20Ready\.\x20Send\x20USER\x20command\.\n")%r(GenericLines,1D
SF:,"OK\x20Ready\.\x20Send\x20USER\x20command\.\n")%r(GetRequest,1D,"OK\x2
SF:0Ready\.\x20Send\x20USER\x20command\.\n")%r(HTTPOptions,1D,"OK\x20Ready
SF:\.\x20Send\x20USER\x20command\.\n")%r(RTSPRequest,1D,"OK\x20Ready\.\x20
SF:Send\x20USER\x20command\.\n")%r(RPCCheck,1D,"OK\x20Ready\.\x20Send\x20U
SF:SER\x20command\.\n")%r(DNSVersionBindReqTCP,1D,"OK\x20Ready\.\x20Send\x
SF:20USER\x20command\.\n")%r(DNSStatusRequestTCP,1D,"OK\x20Ready\.\x20Send
SF:\x20USER\x20command\.\n")%r(Help,1D,"OK\x20Ready\.\x20Send\x20USER\x20c
SF:ommand\.\n")%r(SSLSessionReq,1D,"OK\x20Ready\.\x20Send\x20USER\x20comma
SF:nd\.\n")%r(TerminalServerCookie,1D,"OK\x20Ready\.\x20Send\x20USER\x20co
SF:mmand\.\n")%r(TLSSessionReq,1D,"OK\x20Ready\.\x20Send\x20USER\x20comman
SF:d\.\n")%r(Kerberos,1D,"OK\x20Ready\.\x20Send\x20USER\x20command\.\n")%r
SF:(SMBProgNeg,1D,"OK\x20Ready\.\x20Send\x20USER\x20command\.\n")%r(X11Pro
SF:be,1D,"OK\x20Ready\.\x20Send\x20USER\x20command\.\n")%r(FourOhFourReque
SF:st,1D,"OK\x20Ready\.\x20Send\x20USER\x20command\.\n")%r(LPDString,1D,"O
SF:K\x20Ready\.\x20Send\x20USER\x20command\.\n")%r(LDAPSearchReq,1D,"OK\x2
SF:0Ready\.\x20Send\x20USER\x20command\.\n")%r(LDAPBindReq,1D,"OK\x20Ready
SF:\.\x20Send\x20USER\x20command\.\n")%r(SIPOptions,1D,"OK\x20Ready\.\x20S
SF:end\x20USER\x20command\.\n")%r(LANDesk-RC,1D,"OK\x20Ready\.\x20Send\x20
SF:USER\x20command\.\n")%r(TerminalServer,1D,"OK\x20Ready\.\x20Send\x20USE
SF:R\x20command\.\n")%r(NCP,1D,"OK\x20Ready\.\x20Send\x20USER\x20command\.
SF:\n")%r(NotesRPC,1D,"OK\x20Ready\.\x20Send\x20USER\x20command\.\n")%r(Ja
SF:vaRMI,1D,"OK\x20Ready\.\x20Send\x20USER\x20command\.\n")%r(WMSRequest,1
SF:D,"OK\x20Ready\.\x20Send\x20USER\x20command\.\n")%r(oracle-tns,1D,"OK\x
SF:20Ready\.\x20Send\x20USER\x20command\.\n")%r(ms-sql-s,1D,"OK\x20Ready\.
SF:\x20Send\x20USER\x20command\.\n")%r(afp,1D,"OK\x20Ready\.\x20Send\x20US
SF:ER\x20command\.\n")%r(giop,1D,"OK\x20Ready\.\x20Send\x20USER\x20command
SF:\.\n");

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Jun 21 13:13:22 2021 -- 1 IP address (1 host up) scanned in 367.18 seconds
```