---
title: MBAM 2.5 security considerations
description: This article contains information about how to secure Microsoft BitLocker Administration and Monitoring (MBAM).
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/23/2017
---

# MBAM 2.5 security considerations

This article contains information about how to secure Microsoft BitLocker Administration and Monitoring (MBAM).

## <a href="" id="bkmk-tpm"></a>Configure MBAM to escrow the TPM and store OwnerAuth passwords

> [!NOTE]
> For Windows 10, version 1607 or later, only Windows can take ownership of the TPM. Windows doesn't keep the TPM owner password when it provisions the TPM. For more information, see [TPM owner password](/windows/security/hardware-security/tpm/change-the-tpm-owner-password).

Depending on its configuration, the Trusted Platform Module (TPM) locks itself in certain situations and can remain locked. For example, when a user enters too many incorrect passwords. During TPM lockout, BitLocker can't access the encryption keys to unlock or decrypt the drive. This state requires the user to enter their BitLocker recovery key to access the operating system drive. To reset TPM lockout, you must provide the TPM OwnerAuth password.

MBAM can store the TPM OwnerAuth password in the MBAM database if it owns the TPM or if it escrows the password. OwnerAuth passwords are then easily accessible on the Administration and Monitoring Website when you must recover from a TPM lockout, eliminating the need to wait for the lockout to resolve on its own.

### Escrowing TPM OwnerAuth in Windows 8 and later

> [!NOTE]
> For Windows 10, version 1607 or later, only Windows can take ownership of the TPM. Windows doesn't keep the TPM owner password when it provisions the TPM. For more information, see [TPM owner password](/windows/security/hardware-security/tpm/change-the-tpm-owner-password).

In Windows 8 or higher, MBAM no longer must own the TPM to store the OwnerAuth password, as long as the OwnerAuth is available on the local machine.

To enable MBAM to escrow and then store TPM OwnerAuth passwords, you must configure these group policy settings.

| Group policy setting                                                         | Configuration                  |
|------------------------------------------------------------------------------|--------------------------------|
| Turn on TPM backup to Active Directory Domain Services                       | Disabled or Not Configured     |
| Configure the level of TPM owner authorization information available to the operating system | Delegated/None or Not Configured |

The location of these group policy settings is **Computer Configuration** > **Administrative Templates** > **System** > **Trusted Platform Module Services**.

> [!NOTE]
> Windows removes the OwnerAuth locally after MBAM successfully escrows it with these settings.

### Escrowing TPM OwnerAuth in Windows 7

In Windows 7, MBAM must own the TPM to automatically escrow TPM OwnerAuth information in the MBAM database. If MBAM doesn't own the TPM, you must use the MBAM Active Directory (AD) data import cmdlets to copy TPM OwnerAuth from Active Directory into the MBAM database.

### MBAM Active Directory data import cmdlets

The MBAM Active Directory data import cmdlets let you retrieve recovery key packages and OwnerAuth passwords that are stored in Active Directory.

The MBAM 2.5 SP1 server ships with four PowerShell cmdlets that prepopulate MBAM databases with the volume recovery and TPM owner information stored in Active Directory.

For volume recovery keys and packages:

- Read-ADRecoveryInformation

- Write-MbamRecoveryInformation

For TPM Owner Information:

- Read-ADTpmInformation

- Write-MbamTpmInformation

For Associating Users to Computers:

- Write-MbamComputerUser

The `Read-AD*` cmdlets read information from Active Directory. The `Write-Mbam*` cmdlets push the data into the MBAM databases. For detailed information about these cmdlets, including syntax, parameters, and examples, see [Cmdlet reference for Microsoft BitLocker Administration and Monitoring 2.5](/powershell/mdop/get-started).

**Create user-to-computer associations:** The MBAM Active Directory Data Import cmdlets gather information from Active Directory and insert the data into MBAM database. However, they don't associate users to volumes. You can download the Add-ComputerUser.ps1 PowerShell script to create user-to-machine associations, which let users regain access to a computer through the Administration and Monitoring Website or by using the Self-Service Portal for recovery. The Add-ComputerUser.ps1 script gathers data from the **Managed By** attribute in Active Directory (AD), the object owner in AD, or from a custom CSV file. The script then adds the discovered users to the recovery information pipeline object, which must be passed to Write-MbamRecoveryInformation to insert the data into the recovery database.

You can specify **help Add-ComputerUser.ps1** to get help for the script, including examples of how to use the cmdlets and the script.

To create user-to-computer associations after you install the MBAM server, use the Write-MbamComputerUser PowerShell cmdlet. Similar to the Add-ComputerUser.ps1 PowerShell script, this cmdlet lets you specify users that can use the Self-Service Portal to get TPM OwnerAuth information or volume recovery passwords for the specified computer.

> [!NOTE]
> The MBAM agent overrides user-to-computer associations when that computer begins reporting up to the server.

**Prerequisites:** The `Read-AD*` cmdlets can retrieve information from AD only if they're either run as a highly privileged user account, such as a Domain Administrator, or run as an account in a custom security group granted read access to the information (recommended).

[BitLocker Drive Encryption operations guide: Recovering encrypted volumes with ADDS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771778(v=ws.10)) provides details about creating a custom security group (or multiple groups) with read access to the AD information.

**MBAM Recovery and Hardware Web Service Write Permissions:** The `Write-Mbam*` cmdlets accept the URL of the MBAM Recovery and Hardware Service, used to publish the recovery or TPM information. Typically, only a domain computer service account can communicate with the MBAM Recovery and Hardware Service. In MBAM 2.5 SP1, you can configure the MBAM Recovery and Hardware Service with a security group called DataMigrationAccessGroup. Members of this group can bypass the domain computer service account check. The `Write-Mbam*` cmdlets must be run as a user belonging to this configured group. (Alternatively, the credentials of an individual user in the configured group can be specified by using the -Credential parameter in the `Write-Mbam*` cmdlets.)

You can configure the MBAM Recovery and Hardware Service with the name of this security group in one of these ways:

- Provide the name of the security group (or individual) in the -DataMigrationAccessGroup parameter of the Enable-MbamWebApplication -AgentService PowerShell cmdlet.

- Configure the group after you install the MBAM Recovery and Hardware Service. Edit the web.config file in the `<inetpub>\Microsoft Bitlocker Management Solution\Recovery and Hardware Service\` folder.

    ```xml
    <add key="DataMigrationUsersGroupName" value="<groupName>|<empty>" />
    ```

    where `<groupName>` is replaced with the domain and the group name (or the individual user) that you use to allow data migration from Active Directory.

- To edit this appSetting, use the Configuration Editor in IIS Manager.

In the following example, when you run the command as a member of both the ADRecoveryInformation and Data Migration Users groups, it pulls the volume recovery information from computers in the WORKSTATIONS organizational unit (OU) in the contoso.com domain. It then writes them to MBAM by using the MBAM Recovery and Hardware Service running on the mbam.contoso.com server.

```powershell
Read-ADRecoveryInformation -Server contoso.com -SearchBase "OU=WORKSTATIONS,DC=CONTOSO,DC=COM" | Write-MbamRecoveryInformation -RecoveryServiceEndPoint "https://mbam.contoso.com/MBAMRecoveryAndHardwareService/CoreService.svc"
```

`Read-AD*` cmdlets accept the name or IP address of an Active Directory hosting server machine to query for recovery or TPM information. We recommend providing the distinguished names of the AD containers in which the computer object resides as the value of the SearchBase parameter. If computers are stored across several OUs, the cmdlets can accept pipeline input to run once for each container. The distinguished name of an AD container looks similar to `OU=Machines,DC=contoso,DC=com`.

When you run a search targeted to specific containers, it provides the following benefits:

- Reduces the risk of timeout while querying a large AD dataset for computer objects.

- Can omit OUs containing datacenter servers or other classes of computers for which the backup might not be desired or necessary.

Another option is to provide the -Recurse flag with or without the optional SearchBase to search for computer objects across all containers under the specified SearchBase or the entire domain respectively. When you use the -Recurse flag, you can also use the -MaxPageSize parameter to control the amount of local and remote memory required to service the query.

These cmdlets write to the pipeline objects of type PsObject. Each PsObject instance contains a single volume recovery key or TPM owner string with its associated computer name, timestamp, and other information required to publish it to the MBAM data store.

`Write-Mbam*` cmdlets** accept recovery information parameter values from the pipeline by property name. This behavior allows the `Write-Mbam*` cmdlets to accept the pipeline output of the `Read-AD*` cmdlets. For example, `Read-ADRecoveryInformation -Server contoso.com -Recurse | Write-MbamRecoveryInformation -RecoveryServiceEndpoint mbam.contoso.com`

The `Write-Mbam*` cmdlets include optional parameters that provide options for fault tolerance, verbose logging, and preferences for WhatIf and Confirm.

The `Write-Mbam*` cmdlets also include an optional *Time* parameter whose value is a **DateTime** object. This object includes a *Kind* attribute that can be set to `Local`, `UTC`, or `Unspecified`. When the *Time* parameter is populated from data taken from the Active Directory, the time is converted to UTC and this *Kind* attribute is set automatically to `UTC`. However, when populating the *Time* parameter using another source, such as a text file, you must explicitly set the *Kind* attribute to its appropriate value.

> [!NOTE]
> The `Read-AD*` cmdlets can't discover the user accounts that represent the computer users. User account associations are needed for the following:
>
> - Users to recover volume passwords or packages by using the Self-Service portal.
>
> - Users who aren't in the MBAM Advanced Helpdesk Users security group as defined during installation, recovering on behalf of other users.

## <a href="" id="bkmk-autounlock"></a>Configure MBAM to automatically unlock the TPM after a lockout

You can configure MBAM 2.5 SP1 to automatically unlock the TPM if it's locked out. If TPM lockout auto reset is enabled, MBAM can detect that a user is locked out and then get the OwnerAuth password from the MBAM database to automatically unlock the TPM for the user. TPM lockout auto reset is only available if the OS recovery key for that computer was retrieved by using the Self Service Portal or the Administration and Monitoring Website.

> [!IMPORTANT]
> To enable TPM lockout auto reset, you must configure this feature on both the server side and in group policy on the client side.

- To enable TPM lockout auto reset on the client side, configure the group policy setting "Configure TPM lockout auto reset" located at **Computer Configuration** > **Administrative Templates** > **Windows Components** > **MDOP MBAM** > **Client Management**.

- To enable TPM lockout auto reset on the server side, you can check "Enable TPM lockout auto reset" in the MBAM server Configuration wizard during setup.

    You can also enable TPM lockout auto reset in PowerShell by specifying the `-TPM` "lockout auto reset" switch while enabling the agent service web component.

After a user enters the BitLocker recovery key they obtained from the Self Service Portal or the Administration and Monitoring Website, the MBAM agent will determine if the TPM is locked out. If it's locked out, it attempts to retrieve the TPM OwnerAuth for the computer from the MBAM database. If the TPM OwnerAuth is successfully retrieved, it's used to unlock the TPM. Unlocking the TPM makes the TPM fully functional and the user isn't forced to enter the recovery password during subsequent reboots from a TPM lockout.

TPM lockout auto reset is disabled by default.

> [!NOTE]
> TPM lockout auto reset is only supported on computers running TPM version 1.2. TPM 2.0 provides built-in lockout auto reset functionality.

**The Recovery Audit Report** includes events related to TPM lockout auto reset. If a request is made from the MBAM client to retrieve a TPM OwnerAuth password, an event is logged to indicate recovery. Audit entries include the following events:

| Entry                | Value               |
|----------------------|---------------------|
| Audit Request Source | Agent TPM unlock    |
| Key Type             | TPM Password Hash   |
| Reason Description   | TPM Reset           |

## <a href="" id="bkmk-secure-databases"></a>Secure connections to SQL Server

In MBAM, SQL Server communicates with SQL Server Reporting Services and with the web services for the Administration and Monitoring website and Self-Service Portal. We recommend that you secure the communication with SQL Server. For more information, see [Encrypting connections to SQL Server](/previous-versions/sql/sql-server-2008-r2/ms189067(v=sql.105)).

For more information about securing the MBAM websites, see [Planning how to secure the MBAM websites](planning-how-to-secure-the-mbam-websites.md).

## <a href="" id="bkmk-accts-groups"></a>Create accounts and groups

The best practice for managing user accounts is to create domain global groups and add user accounts to them. For a description of the recommended accounts and groups, see [Planning for MBAM 2.5 groups and accounts](planning-for-mbam-25-groups-and-accounts.md).

## <a href="" id="bkmk-logfiles"></a>Use MBAM log files

This section describes the MBAM server and MBAM client log files.

### MBAM server setup log files

The **MBAMServerSetup.exe** file generates the following log files in the user's **%temp%** folder during the MBAM installation:

- `Microsoft_BitLocker_Administration_and_Monitoring_<14 numbers>.log`

    Logs the actions during the MBAM setup and the MBAM server feature configuration.

- `Microsoft_BitLocker_Administration_and_Monitoring_<14_numbers>_0_MBAMServer.msi.log`

    Logs other actions during installation.

### MBAM server configuration log files

- `Applications and Services Logs/Microsoft Windows/MBAM-Setup`

    Logs any errors when you use Windows PowerShell cmdlets or the MBAM server configuration wizard to configure the MBAM server features.

### MBAM client setup log files

- `MSI<five random characters>.log`

    Logs the actions taken during the MBAM client installation.

### MBAM-Web log files

- Shows activity from the web portals and services.

## <a href="" id="bkmk-tde"></a>Review MBAM database TDE considerations

The transparent data encryption (TDE) feature that is available in SQL Server is an optional installation for the database instances that host the MBAM database features.

With TDE, you can perform real-time, full database-level encryption. TDE is the optimal choice for bulk encryption to meet regulatory compliance or corporate data security standards. TDE works at the file level, which is similar to two Windows features: the Encrypting File System (EFS) and BitLocker Drive Encryption. Both features also encrypt data on the hard drive. TDE doesn't replace cell-level encryption, EFS, or BitLocker.

When TDE is enabled on a database, all backups are encrypted. Thus, special care must be taken to ensure that the certificate that was used to protect the database encryption key is backed up and maintained with the database backup. If this certificate is lost, the data is unreadable.

Back up the certificate with the database. Each certificate backup should have two files. Both of these files should be archived. Ideally for security, they should be backed up separately from the database backup file. You can alternatively consider using the extensible key management (EKM) feature for storage and maintenance of keys that are used for TDE.

For an example of how to enable TDE for MBAM database instances, see [Transparent data encryption (TDE)](/sql/relational-databases/security/encryption/transparent-data-encryption).

## <a href="" id="bkmk-general-security"></a>Understand general security considerations

- **Understand the security risks.** The most serious risk when you use MBAM is that its functionality could be compromised by an unauthorized user. This user could then reconfigure BitLocker Drive Encryption and gain BitLocker encryption key data on MBAM clients. The loss of MBAM functionality for a short period of time due to a denial-of-service attack doesn't generally have a catastrophic effect.

- **Physically secure your computers**. There's no security without physical security. An attacker who gets physical access to an MBAM server could potentially use it to attack the entire client base. All potential physical attacks must be considered high risk and mitigated appropriately. MBAM servers should be stored in a secure server room with controlled access. Secure these computers when administrators aren't physically present by having the operating system lock the computer, or by using a secured screen saver.

- **Apply the most recent security updates to all computers**.

- **Use strong passwords or pass phrases**. Always use strong passwords with 15 or more characters for all MBAM administrator accounts. Never use blank passwords. For more information about password concepts, see [Password policy](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh994572(v=ws.11)).

## Related articles

[Planning to deploy MBAM 2.5](planning-to-deploy-mbam-25.md)
