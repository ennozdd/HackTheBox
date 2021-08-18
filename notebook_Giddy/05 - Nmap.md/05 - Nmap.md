# 05 - Nmap


```sql
# Nmap 7.91 scan initiated Tue Aug 17 19:48:07 2021 as: nmap -sV -sC -p- -oA nmap/giddy -vvv 10.10.10.104
Nmap scan report for 10.10.10.104
Host is up, received echo-reply ttl 127 (0.077s latency).
Scanned at 2021-08-17 19:48:07 +03 for 221s
Not shown: 65531 filtered ports
Reason: 65531 no-responses
PORT     STATE SERVICE       REASON          VERSION
80/tcp   open  http          syn-ack ttl 127 Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
443/tcp  open  ssl/http      syn-ack ttl 127 Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
| ssl-cert: Subject: commonName=PowerShellWebAccessTestWebSite
| Issuer: commonName=PowerShellWebAccessTestWebSite
| Public Key type: rsa
| Public Key bits: 1024
| Signature Algorithm: sha1WithRSAEncryption
| Not valid before: 2018-06-16T21:28:55
| Not valid after:  2018-09-14T21:28:55
| MD5:   78a7 4af5 3b09 c882 a149 f977 cf8f 1182
| SHA-1: 8adc 3379 878a f13f 0154 406a 3ead d345 6967 6a23
| -----BEGIN CERTIFICATE-----
| MIICHTCCAYagAwIBAgIQG2rbVjzfZqJIr005rMK4xTANBgkqhkiG9w0BAQUFADAp
| MScwJQYDVQQDDB5Qb3dlclNoZWxsV2ViQWNjZXNzVGVzdFdlYlNpdGUwHhcNMTgw
| NjE2MjEyODU1WhcNMTgwOTE0MjEyODU1WjApMScwJQYDVQQDDB5Qb3dlclNoZWxs
| V2ViQWNjZXNzVGVzdFdlYlNpdGUwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGB
| ALOvHao3JEpJzzBHR9oCc+934QLPu2vRlC7jZAwySPX6v6fkvzsDr7uD50maLVtW
| 9etn9KVwfmgkYd6YtY+86YCc935s1rppNtNKeVXsG/PM4G+4HdPFf1Ik3Vj6fc1y
| w1nx2PLSNvlC74kkc33MA8y//vxqIckSJiHiVa5ZzdR/AgMBAAGjRjBEMBMGA1Ud
| JQQMMAoGCCsGAQUFBwMBMB0GA1UdDgQWBBS4T3PavA05OLCMaCa6GqgXsjCoozAO
| BgNVHQ8BAf8EBAMCBSAwDQYJKoZIhvcNAQEFBQADgYEAm6FzHooZ+SSLNp9KvPdX
| jjFPpf9Jv4j8Ao9qv1RnbwmTE5SSHhusXDOiAIOsErTVdaNa0VRcduMt+H054kfp
| 1MeoYvKXuXlMLbGe+orEIiVPjC/7cTJIVyfgyhdl5PdtetlZGrspK8h+2QqvxXpF
| im+bXy93yFQ6G9tOrzpBmFY=
|_-----END CERTIFICATE-----
|_ssl-date: 2021-08-17T16:51:47+00:00; 0s from scanner time.
| tls-alpn: 
|   h2
|_  http/1.1
3389/tcp open  ms-wbt-server syn-ack ttl 127 Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: GIDDY
|   NetBIOS_Domain_Name: GIDDY
|   NetBIOS_Computer_Name: GIDDY
|   DNS_Domain_Name: Giddy
|   DNS_Computer_Name: Giddy
|   Product_Version: 10.0.14393
|_  System_Time: 2021-08-17T16:51:44+00:00
| ssl-cert: Subject: commonName=Giddy
| Issuer: commonName=Giddy
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2021-05-03T14:56:04
| Not valid after:  2021-11-02T14:56:04
| MD5:   aa42 a9f1 1181 e790 9d59 28dd 7879 5878
| SHA-1: f5ac fe1b ea5a 81ad a917 c1c2 0087 90a8 1bed 5dc5
| -----BEGIN CERTIFICATE-----
| MIICzjCCAbagAwIBAgIQK+5iOcFviIRC7dJEQu8vgzANBgkqhkiG9w0BAQsFADAQ
| MQ4wDAYDVQQDEwVHaWRkeTAeFw0yMTA1MDMxNDU2MDRaFw0yMTExMDIxNDU2MDRa
| MBAxDjAMBgNVBAMTBUdpZGR5MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKC
| AQEA5Bgf2PftkCXC7u2ritXcfTPd1D31JlFGBYwb3peCp0Gd0hqlVybPKS2UrCFz
| wSiBRSQUmWka2b93ZX6bLKsDk8KAwSVdWztR55paVdG6GPBQS5JKMvWF8sK92074
| xelawc0fjFRgNlQrABbgO9ENNshUOctSsUp+6HrbKwX2fzRxOhVxt16VdTBGkYcN
| hNaRkb6T/dyjMn57SBazdP448LK44wn7U3Cs4ABfnygcuaGSufBSWWAtEwran3wj
| zgHBhgpC1UN2EyiIpHUvZKoFPyvmlqipjSny9LwFEwT6FLloxBH00xASgT01/7J8
| JXAk125KV84aDNVpzcaaiHJbMQIDAQABoyQwIjATBgNVHSUEDDAKBggrBgEFBQcD
| ATALBgNVHQ8EBAMCBDAwDQYJKoZIhvcNAQELBQADggEBALOi5I7aJWpGZgtu283x
| 9iEfozsQxGreAiF0ls9VVkExwoqa5CsyZZkxXbYxlWZLZByynqbCFuEzgKP69/Wf
| PpodT3nhsg8P77EoU+vhPZeZxzcbaCyla44s1NFQom0c45oSKyQ0lK6VpvjkRJtl
| 944hHbioRiqdrdn/MyC7DW4J7FoHJSj/O9Qx9mbMy8qE30W4IqnGuRIhnb9Fl0vx
| fRvG215mkZwYjZ7l74IlRajRMWKdq/f3JgHlT2UVZJwzPjgfvMqJYOoiebBwQOHx
| WZtBIWeHRFgfl4HYeM0EtRieTYQ5pdwARm/r2VKX8HOa7gAX99lQz7XsCkRpcktA
| Y70=
|_-----END CERTIFICATE-----
|_ssl-date: 2021-08-17T16:51:47+00:00; 0s from scanner time.
5985/tcp open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 0s, deviation: 0s, median: 0s

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Aug 17 19:51:48 2021 -- 1 IP address (1 host up) scanned in 221.15 seconds
```