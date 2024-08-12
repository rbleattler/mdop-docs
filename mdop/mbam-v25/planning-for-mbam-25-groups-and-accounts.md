---
title: Planning for MBAM 2.5 groups and accounts
description: This article lists the roles and accounts that you must create in Active Directory Domain Services to provide security and access rights for the Microsoft BitLocker Administration and Monitoring (MBAM) databases, reports, and web applications.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 11/02/2016
---

# Planning for MBAM 2.5 groups and accounts

This article lists the roles and accounts that you must create in Active Directory Domain Services to provide security and access rights for the Microsoft BitLocker Administration and Monitoring (MBAM) databases, reports, and web applications. For each role and account, the corresponding field in the MBAM Server Configuration wizard is provided. For a list of Windows PowerShell cmdlets and parameters that correspond to these accounts, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md#bkmk-reqd-posh-accts).

> [!NOTE]
> MBAM doesn't support the use of managed service accounts.

## Database accounts

Create the following accounts for the Compliance and Audit Database and the Recovery Database.

| Account name and purpose | Account type | MBAM Server Configuration wizard field that corresponds to this account | Description of the MBAM Server Configuration wizard field that corresponds to this account |
|--|--|--|--|
| Compliance and Audit Database and Recovery Database read/write user or group for reports | User or Group | Read/write access domain user or group | Domain user or group that has read/write access to the Compliance and Audit Database and the Recovery Database to enable the web applications to access the data and reports in these databases.<br>If you enter a user name in this field, it must be the same value as the value in the **Web service application pool domain account** field on the **Configure Web Applications** page.<br>If you enter a group name in this field, the value in the **Web service application pool domain account** field on the **Configure Web Applications** page must be a member of the group you enter in this field. |
| Compliance and Audit Database read-only user or group for reports | User or Group | Read-only access domain user or group | Name of the user or group that has read-only access to the Compliance and Audit Database to enable the reports to access the compliance and audit data in this database.<br>If you enter a user name in this field, it must be the same user as the one you specify in the **Compliance and Audit Database domain account** field on the **Configure Reports** page.<br>If you enter a group name in this field, the value that you specify in the **Compliance and Audit Database domain account** field on the **Configure Reports** page must be a member of the group that you specify in this field. |

## Reporting accounts

Create the following accounts for the Reports feature.

| Account name/purpose | Account type | MBAM Server Configuration wizard field that corresponds to this account | Description of the MBAM Server Configuration wizard field that corresponds to this account |
|--|--|--|--|
| Reports read-only domain access group | Group | Reporting role domain group | Specifies the domain user group that has read-only access to the reports in the Administration and Monitoring Website. The group you specify must be the same group you specified for the Reports Read Only Access Group parameter when the web apps are enabled. |
| Compliance and Audit Database domain user account | User | Compliance and Audit Database domain account | Domain user account and password that the local SQL Server Reporting Services instance uses to access the Compliance and Audit Database. This account requires **Log On as Batch** rights to the SQL Server Reporting Services server.<br>If the value you enter in the **Read-only access domain user or group** field on the **Configure Databases** page is a user name, you must enter that same value in this field.<br>If the value you enter in the **Read-only access domain user or group** field on the **Configure Databases** page is a group name, the value that you enter in this field must be a member of that group.<br>Configure the password for this account to never expire. The user account should be able to access all data that is available to the MBAM Reports Users group. |

## <a href="" id="bkmk-helpdesk-roles"></a>Administration and Monitoring Website (Help Desk) accounts

Create the following accounts for the Administration and Monitoring Website.

| Account name/purpose | Account type | MBAM Server Configuration wizard field that corresponds to this account | Description of the MBAM Server Configuration wizard field that corresponds to this account |
|--|--|--|--|
| Web service application pool domain account | User | Web service application pool domain account | Domain user account to be used by the application pool for the web applications.<br>If you enter a user name in the **Read/write access domain user or group** field on the **Configure Databases** page, you must enter that same value in this field.<br>If you enter a group name in the **Read/write access domain user or group** field on the **Configure Databases** page, the value you enter in this field must be a member of that group.<br>If you don't specify credentials, the credentials that were specified for any previously enabled web application are used. All web applications must use the same application pool credentials. If you specify different credentials for different web applications, the most recently specified value is used.<br>**Important**: For improved security, set the account that is specified in the credentials to have limited user rights. |
| MBAM Advanced Helpdesk Users access group | Group | MBAM Advanced Helpdesk Users | Domain user group whose members have access to all recovery areas of the Administration and Monitoring Website. Users who have this role have to enter only the recovery key, and not the end user's domain and user name, when helping end users recover their drives. If a user is a member of both the MBAM Helpdesk Users group and the MBAM Advanced Helpdesk Users group, the MBAM Advanced Helpdesk Users group permissions override the MBAM Helpdesk Group permissions. |
| MBAM Helpdesk Users access group | Group | MBAM Helpdesk Users | Domain user group whose members have access to the Manage TPM and Drive Recovery areas of the MBAM Administration and Monitoring Website. Individuals who have this role must fill in all fields, including the end-user's domain and account name, when they use either option.<br>If a user is a member of both the MBAM Helpdesk Users group and the MBAM Advanced Helpdesk Users group, the MBAM Advanced Helpdesk Users group permissions override the MBAM Helpdesk Group permissions. |
| MBAM Report Users access group | Group | MBAM Report Users | Domain user group whose members have read-only access to the reports in the Reports area of the Administration and Monitoring Website. |
| MBAM Data Migration User Group | Group | MBAM Data Migration Users | Optional domain user group whose members have permissions to write data to MBAM by using the MBAM Recovery and Hardware Service running on the MBAM server. This account is used with the `Write-Mbam*` cmdlets to write recovery and TPM data from Active Directory into the MBAM database.<br>For more information, see [MBAM 2.5 security considerations](mbam-25-security-considerations.md). |

## Related articles

[Preparing your environment for MBAM 2.5](preparing-your-environment-for-mbam-25.md)

[MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md)
