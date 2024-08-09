---
title: Configuring MBAM 2.5 server features by using Windows PowerShell
description: After you install the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 server software, you can configure MBAM 2.5 server features by using Windows PowerShell cmdlets or the MBAM Server Configuration wizard.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Configuring MBAM 2.5 server features by using Windows PowerShell

After you install the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 server software, you can configure MBAM 2.5 server features by using Windows PowerShell cmdlets or the MBAM Server Configuration wizard. This article describes how to configure MBAM 2.5 by using the Windows PowerShell cmdlets. To use the wizard instead, see [Configuring the MBAM 2.5 Server Features](configuring-the-mbam-25-server-features.md).

For information about the **Get-MbamBitLockerRecoveryKey** and **Get-MbamTPMOwnerPassword** Windows PowerShell cmdlets, which are used to administer MBAM, see [Using Windows PowerShell to Administer MBAM 2.5](using-windows-powershell-to-administer-mbam-25.md).

## <a href="" id="bkmk-load-posh-help"></a>How to load Windows PowerShell help for MBAM 2.5

For a list of the Windows PowerShell cmdlets on TechNet, see [Microsoft Desktop Optimization Pack automation with Windows PowerShell](/powershell/mdop/get-started).

### To load the MBAM 2.5 help for Windows PowerShell cmdlets after installing the MBAM server software

1.  Open Windows PowerShell or Windows PowerShell Integrated Scripting Environment (ISE).

2.  Type `Update-Help -Module Microsoft.MBAM`

## <a href="" id="bkmk-help-specific-cmdlet"></a>How to get help about an MBAM Windows PowerShell cmdlet

Windows PowerShell help for MBAM is available in the following formats:

- At a Windows PowerShell command prompt, type `Get-Help <cmdlet>`
  - To upload the latest Windows PowerShell cmdlets, follow the instructions in the previous section on how to load Windows PowerShell help for MBAM.
- [Get started with MDOP automation](/powershell/mdop/get-started)
- [Download MDOP cmdlet reference documentation](https://www.microsoft.com/download/details.aspx?id=41195)

## <a href="" id="bkmk-config-only-posh"></a>Configurations that you can do only with Windows PowerShell but not with the MBAM Server Configuration wizard

| Configurations that you can do only by using Windows PowerShell | Details |
|--|--|
| Install the web services on a separate computer from the web applications. | Using the wizard, you must install the web services and web applications on the same computer. |
| Enable reports on a separate reporting services point without installing all of the Configuration Manager objects. |  |
| Delete all of the objects from Configuration Manager. | Deleting the objects in turn deletes all of the compliance data from Configuration Manager. |
| Enter a custom connection string for the databases. | Example: To configure the web applications to work with mirroring, you must use the **Enable-MbamWebApplication** cmdlet to specify the appropriate failover partner syntax in the connection string. |
| Skip validation and configure a feature even though the prerequisite check failed. |  |

> [!NOTE]
> You can't disable the MBAM databases with a Windows PowerShell cmdlet or the MBAM Server Configuration wizard. To prevent the accidental removal of your compliance and audit data, database administrators must remove databases manually.

## <a href="" id="bkmk-prereqs-posh-mbamsvr"></a>Prerequisites and requirements for using Windows PowerShell to configure MBAM server features

Before starting the configuration, complete the following prerequisites.

### Account-related prerequisites

| Prerequisite | Details or additional information |
|--|--|
| Create the required accounts. | See section **Required accounts and corresponding Windows PowerShell cmdlet parameters** later in this article. |
| User accounts and groups that you pass as parameters to the Windows PowerShell cmdlets must be valid accounts in the domain. | You can't use local accounts. |
| Specify accounts in the down-level format. | Examples:<br>`domainNetBiosName\user`<br>`domainNetBiosName\group` |

### Permission-related prerequisites

- You must be an administrator on the local computer where you're configuring the MBAM feature.
- Use an elevated Windows PowerShell command prompt to run all Windows PowerShell cmdlets.

For the **Enable-MbamDatabase** cmdlet only:

- You must have "create any database" permissions on the instance of the target Microsoft SQL Server database.
- By default, the database administrator or system administrator has the required "create any database" permissions.
- This user account must be a part of the local administrators group or the Backup Operators group to register the MBAM Volume Shadow Copy Service (VSS) Writer.
- For more information about VSS Writer, see [Volume Shadow Copy Service](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd364794(v=ws.10)).

For the **System Center Configuration Manager Integration** feature only, the user who enables this feature must have these rights in Configuration Manager:

| Type of rights in Configuration Manager                | Required rights                                      |
|--------------------------------------------------------|------------------------------------------------------|
| Configuration Manager Site rights:                     | - Read                                               |
| Configuration Manager Collection rights:               | - Create<br>- Delete<br>- Read<br>- Modify<br>- Deploy Configuration Items |
| Configuration Manager Configuration item rights:       | - Create<br>- Delete<br>- Read                       |

## <a href="" id="bkmk-remote-config"></a>Using Windows PowerShell to configure MBAM on a remote computer

| Capability | Details |
|----------------|-------------|
| **When to use this capability** | When you want to configure the MBAM 2.5 Server features on a remote computer. The Windows PowerShell cmdlets are running on one computer, and you're configuring the features on a different, remote computer. |
| **What you have to do** | To use Windows PowerShell to configure MBAM 2.5 Server features on a remote computer, you must: <ul><li>Ensure that the MBAM 2.5 Server software has been installed on the remote computer.</li><li>Use the Credential Security Support Provider (CredSSP) Protocol to open the Windows PowerShell session.</li><li>Enable Windows Remote Management (WinRM). If you fail to enable WinRM and to configure it correctly, the **New-PSSession** cmdlet that is described in this table displays an error and describes how to fix the issue. For more information about WinRM, see [Using Windows Remote Management](/windows/win32/winrm/using-windows-remote-management).</li></ul> |
| **Why you have to do it** | This protocol enables the Windows PowerShell cmdlets to connect to Active Directory Domain Services by using the user's administrative credentials. You might get a validation error if you start the Windows PowerShell session without this protocol. |
| **How to start a Windows PowerShell session with the CredSSP protocol** | Type the following code at the Windows PowerShell prompt: <br>`$s = New-PSSession -ComputerName xxx -Authentication Credssp -Credential xxx`<br>The following code shows an example:<br>`$session = New-PSSession -ComputerName &lt;MBAM_server_name&gt; -Authentication Credssp -Credential (Get-Credential)`<br>`Enter-PSSession $session` |

## <a href="" id="bkmk-reqd-posh-accts"></a>Required accounts and corresponding Windows PowerShell cmdlet parameters

The following sections describe the accounts that are required to configure MBAM 2.5 server features. It also lists the corresponding Windows PowerShell cmdlet and parameter for which you have to specify the account during configuration.

Cmdlet
Parameter
Type (User or Group)
Description

### Enable-MBAMDatabase

#### AccessAccount

Type: User or Group

Specify a domain user or group that has read/write permission to this database to give the web applications access to data and reports in this database. If the value is a domain user, then the **WebServiceApplicationPoolCredential** parameter that is used when running the **Enable-MbamWebApplication** cmdlet must use the same user account. If the value is a domain Users group, then the domain account that is used by the **WebServiceApplicationPoolCredential** parameter must be a member of this group.

#### ReportAccount

Type: User or Group

Specify a domain user or Users group that has read-only permission to this database to provide the MBAM reports access to the compliance and audit data. If the value is a domain user, then the **ComplianceAndAuditDBCredential** parameter of the **Enable-MbamReport** cmdlet must use the same user account. If the value is a domain Users group, then the domain account that is used by the **ComplianceAndAuditDBCredential** parameter must be a member of this group.

### Enable-MbamReport

#### ComplianceAndAuditDBCredential

Type: User

Specifies the administrative credential that the local SSRS instance uses to connect to the MBAM Compliance and Audit Database. The domain user in the administrative credential must be the same as the user account that is used for the **ReportAccount** parameter, which is used while running the **Enable-MbamDatabase** cmdlet. If a domain Users group was used with the **ReportAccount** parameter, this account should be a member of that group.

> [!IMPORTANT]
> The account specified in the administrative credentials should have limited user rights for improved security. Also, the password of the account should be set to not expire.

#### ReportsReadOnlyAccessGroup

Type: Group

Specifies the domain user group that has read permissions to the reports. The specified group must be the same group that is used for the **ReportsReadOnlyAccessGroup** parameter in the **Enable-MbamWebApplication** cmdlet.

### Enable-MBAMWebApplication

#### AdvancedHelpdeskAccessGroup

Type: Group

Specifies the domain Users group that has access to all areas of the Administration and Monitoring Website except the Reports area.

#### HelpdeskAccessGroup

Type: Group

Specifies the domain Users group that has access to the **Manage TPM** and **Drive Recovery** areas of the Administration and Monitoring Website.

#### ReportsReadOnlyAccessGroup

Type: Group

Specifies the domain Users group that has read permission to the **Reports** area of the Administration and Monitoring Website. The specified group must be the same group that is used for the **ReportsReadOnlyAccessGroup** parameter in the **Enable-MbamReport** cmdlet.

#### WebServiceApplicationPoolCredential

Type: User

Specifies the domain user to be used by the application pool for the MBAM web applications. It must be the same domain user account that is specified in the **AccessAccount** parameter of the **Enable-MbamDatabase** cmdlet. If a domain Users group was used by the **AccessAccount** parameter when running the **Enable-MbamDatabase** cmdlet, the domain user that is specified here must be a member of that group. If you don't specify the administrative credentials, the administrative credentials that were specified by any previously enabled web application are used. All of the web applications use the same application pool identity. If it's specified multiple times, the most recently specified value is used.

> [!IMPORTANT]
> For improved security, set the account that is specified in the administrative credentials to limited user rights. Also, set the password of the account to never expire. Ensure that either the built-in IIS\_IUSRS account or the account that is used for the **WebServiceApplicationPoolCredential** parameter has been added to the **Impersonate a client after authentication** local security setting.
>
> To view the local security setting, open the **Local Security Policy editor**, expand the **Local Policies** node, select the **User Rights Assignment** node, and then double-click the **Impersonate a client after authentication** and **Log on as a batch job** group policy settings in the details pane.

## Related articles

[Configuring the MBAM 2.5 server features](configuring-the-mbam-25-server-features.md)

[Validating the MBAM 2.5 server feature configuration](validating-the-mbam-25-server-feature-configuration.md)

[Using Windows PowerShell to administer MBAM 2.5](using-windows-powershell-to-administer-mbam-25.md)
