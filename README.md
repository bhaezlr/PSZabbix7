# What is PSZabbix7

A powershell module for automating Zabbix administration.

# Goals

This module aims at making it easy to automate the creation of standard 
objects inside Zabbix. That way, Zabbix can be included inside fully 
automated workflows like server provisioning. It may for example be used 
inside a script task of SCVMM to reference a new VM inside Zabbix after 
creation, or to add a newly created user (by your preferred provisioning 
tool) to a set of user groups.

The objects which can be managed are only the basic objects: hosts, host 
groups, users, user groups, templates and a few others. The module does not
expose the full Zabbix API. We actually expect administrators to use the
Zabbix UI to do complex operations like adding monitored items to hosts or
templates (moreover, these operations being rare, there is little value in
automating them). 

This module is tested on Zabbix 7.0.10 and later. Without garantee it could work with versions between 7.0 and 7.0.10
It will not work with older versions.

# Installation

The module is published on the PowerShell gallery, so download and installation is simply (powershell 5+):

```
PS> Install-Module PSZabbix7 -scope CurrentUser
```

If using an older version of PowerShell, you must download the release from the releases page, unzip it 
and put the PSZabbix folder inside MyDocuments/WindowsPowerShell/Modules or any other folder in the module 
search path.

# Usage

All cmdlets have a "get-help" documentation. Here are the basics:

```
# Import the module (if old powershell version)
PS> Import-Module PSZabbix7

# You must first create a session against a Zabbix server - only needed once per work session.
PS> $s = New-ZbxApiSession "http://myserver/zabbix/api_jsonrpc.php" (Get-Credential MyAdminLogin)

# Then call any cmdlet
PS> Get-ZbxHost
hostid host                    name                                        status
------ ----                    ----                                        ------
 10084 Zabbix server           Zabbix server                               Enabled
 10105 Agent Mongo 1           Agent Mongo 1                               Enabled
...

# List of cmdlets (the Zbx prefix can be changed on import if needed):
PS> Get-Command -Module PSZabbix7
CommandType     Name                                               Version    Source                                                                                                                                                                             
-----------     ----                                               -------    ------                                                                                                                                                                             
Function        Add-ZbxHostGroupMembership                         1.3.1      PSZabbix7                                                                                                                                                                          
Function        Add-ZbxHostMacro                                   1.3.1      PSZabbix7                                                                                                                                                                          
Function        Add-ZbxHostTemplate                                1.3.1      PSZabbix7                                                                                                                                                                          
Function        Add-ZbxUserGroupMembership                         1.3.1      PSZabbix7                                                                                                                                                                          
Function        Add-ZbxUserGroupPermission                         1.3.1      PSZabbix7                                                                                                                                                                          
Function        Add-ZbxUserMail                                    1.3.1      PSZabbix7                                                                                                                                                                          
Function        Close-ZbxApiSession                                1.3.1      PSZabbix7                                                                                                                                                                          
Function        Disable-ZbxHost                                    1.3.1      PSZabbix7                                                                                                                                                                          
Function        Disable-ZbxUserGroup                               1.3.1      PSZabbix7                                                                                                                                                                          
Function        Enable-ZbxHost                                     1.3.1      PSZabbix7                                                                                                                                                                          
Function        Enable-ZbxUserGroup                                1.3.1      PSZabbix7                                                                                                                                                                          
Function        Get-ZbxAction                                      1.3.1      PSZabbix7                                                                                                                                                                          
Function        Get-ZbxHost                                        1.3.1      PSZabbix7                                                                                                                                                                          
Function        Get-ZbxHostGroup                                   1.3.1      PSZabbix7                                                                                                                                                                          
Function	Get-ZbxHostGroupHosts                              1.3.1      PSZabbix7
Function        Get-ZbxHostItems                                   1.3.1      PSZabbix7                                                                                                                                                                          
Function        Get-ZbxInterface                                   1.3.1      PSZabbix7                                                                                                                                                                          
Function        Get-ZbxMedia                                       1.3.1      PSZabbix7                                                                                                                                                                          
Function        Get-ZbxMediaType                                   1.3.1      PSZabbix7                                                                                                                                                                          
Function        Get-ZbxProxy                                       1.3.1      PSZabbix7                                                                                                                                                                          
Function        Get-ZbxTemplate                                    1.3.1      PSZabbix7                                                                                                                                                                          
Function        Get-ZbxUser                                        1.3.1      PSZabbix7                                                                                                                                                                          
Function        Get-ZbxUserGroup                                   1.3.1      PSZabbix7                                                                                                                                                                          
Function        New-ZbxApiSession                                  1.3.1      PSZabbix7                                                                                                                                                                          
Function        New-ZbxHost                                        1.3.1      PSZabbix7                                                                                                                                                                          
Function        New-ZbxHostGroup                                   1.3.1      PSZabbix7                                                                                                                                                                          
Function        New-ZbxUser                                        1.3.1      PSZabbix7                                                                                                                                                                          
Function        New-ZbxUserGroup                                   1.3.1      PSZabbix7                                                                                                                                                                          
Function        New-ZbxUserGroupHostgroups                         1.3.1      PSZabbix7                                                                                                                                                                          
Function        New-ZbxUserGroupUsers                              1.3.1      PSZabbix7                                                                                                                                                                          
Function        Remove-ZbxHost                                     1.3.1      PSZabbix7                                                                                                                                                                          
Function        Remove-ZbxHostGroup                                1.3.1      PSZabbix7                                                                                                                                                                          
Function        Remove-ZbxHostGroupMembership                      1.3.1      PSZabbix7                                                                                                                                                                          
Function        Remove-ZbxMedia                                    1.3.1      PSZabbix7                                                                                                                                                                          
Function        Remove-ZbxTemplate                                 1.3.1      PSZabbix7                                                                                                                                                                          
Function        Remove-ZbxUser                                     1.3.1      PSZabbix7                                                                                                                                                                          
Function        Remove-ZbxUserGroup                                1.3.1      PSZabbix7                                                                                                                                                                          
Function        Remove-ZbxUserGroupMembership                      1.3.1      PSZabbix7                                                                                                                                                                          
Function        Update-ZbxHost                                     1.3.1      PSZabbix7                                                                                                                                                                          
Function        Update-ZbxHostInventory                            1.3.1      PSZabbix7                                                                                                                                                                          
Function        Update-ZbxInterface                                1.3.1      PSZabbix7                                                                                                                                                                          
```
