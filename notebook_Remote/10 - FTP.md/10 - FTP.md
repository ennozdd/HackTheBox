# 10 - FTP



# Anonymous access allowed

```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/remote]
└──╼ $ ftp 10.10.10.180
Connected to 10.10.10.180.
220 Microsoft FTP Service
Name (10.10.10.180:user): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password:
230 User logged in.
Remote system type is Windows_NT.
ftp> 
ftp> ls -la
200 PORT command successful.
125 Data connection already open; Transfer starting.
226 Transfer complete.
```

There is no files in here and it is not writable. If ftp was writable, we could try to upload a reverse shell in case it's located somewhere in the web directory, hitting that on http would give us an easy shell.