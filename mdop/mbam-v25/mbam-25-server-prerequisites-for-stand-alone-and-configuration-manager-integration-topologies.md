---
title: MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies
description: Before starting the Microsoft BitLocker Administration and Monitoring (MBAM) installation, you must complete the prerequisites listed in this article.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies

Before starting the Microsoft BitLocker Administration and Monitoring (MBAM) installation, you must complete the prerequisites listed in this article. These prerequisites apply to the MBAM Stand-alone topology and System Center Configuration Manager Integration topology.

If you're deploying MBAM with System Center Configuration Manager, you must complete other prerequisites, which are listed in [MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology](mbam-25-server-prerequisites-that-apply-only-to-the-configuration-manager-integration-topology.md).

For a list of the supported hardware and operating systems for MBAM, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).

> [!IMPORTANT]
> If BitLocker was used without MBAM, you must decrypt the drive and then clear TPM using tpm.msc. If the device is already encrypted and the TPM owner password created, MBAM can't take ownership of TPM.

## Required MBAM roles and accounts

For more information on the groups created in Active Directory Domain Services (ADDS), see [Planning for MBAM 2.5 groups and accounts](planning-for-mbam-25-groups-and-accounts.md).

## Prerequisites for the recovery database

| Prerequisite | Details |
|--------------|---------|
| Supported version of SQL Server | Install Microsoft SQL Server with SQL_Latin1_General_CP1_CI_AS collation.<br>See [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md) for supported versions. |
| Required SQL Server permissions | Required permissions:<br>- SQL Server instance login server roles:<br>  - `dbcreator`<br>  - `processadmin`<br>- SQL Server Reporting Services instance rights:<br>  - Create Folders<br>  - Publish Reports |
| Optional - Install the Transparent Data Encryption (TDE) feature available in SQL Server | The TDE SQL Server feature performs real-time I/O encryption and decryption of the data and log files, which can help you to comply with laws, regulations, and guidelines that apply to various industries.<br>**Note:** TDE performs real-time decryption of database information. If you view recovery key information in the SQL Server database, and you're signed in under an account that has permissions to the database, the recovery key information is visible. To read more about TDE, see [MBAM 2.5 security considerations](mbam-25-security-considerations.md). |
| SQL Server Database Engine Services | SQL Server Database Engine Services must be installed and running during MBAM Server installation. |
| Windows PowerShell 3.0 or later | Windows PowerShell doesn't have to be installed on the Recovery Database server if you're using Windows PowerShell to configure the database from a remote computer. |

## Prerequisites for the compliance and audit database

| Prerequisite | Details |
|--------------|---------|
| Supported version of SQL Server | Install SQL Server with SQL_Latin1_General_CP1_CI_AS collation.<br>See [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md) for supported versions. |
| Required SQL Server permissions | Required permissions:<br>- SQL Server instance login server roles:<br>  - `dbcreator`<br>  - `processadmin`<br>- SQL Server Reporting Services instance rights:<br>  - Create Folders<br>  - Publish Reports |
| Optional - Install the Transparent Data Encryption (TDE) feature in SQL Server | The TDE SQL Server feature performs real-time I/O encryption and decryption of the data and log files, which can help you to comply with laws, regulations, and guidelines that apply to various industries.<br>TDE performs real-time decryption of database information. This means that, if you view recovery key information in the SQL Server database, and you're signed in under an account that has permissions to the database, the recovery key information is visible. To read more about TDE, see [MBAM 2.5 security considerations](mbam-25-security-considerations.md). |
| SQL Server Database Engine Services | SQL Server Database Engine Services must be installed and running during MBAM Server installation. However, SQL Server can be running remotely; it doesn't have to be on the same server on which you're installing the MBAM Server software. |
| Windows PowerShell 3.0 or later | Windows PowerShell doesn't have to be installed on the Compliance and Audit Database server if you're using Windows PowerShell to configure the database from a remote computer. |

## Prerequisites for the reports

| Prerequisite | Details |
|--------------|---------|
| Supported version of SQL Server | Install SQL Server with SQL_Latin1_General_CP1_CI_AS collation.<br>See [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md) for supported versions. |
| SQL Server Reporting Services (SSRS) | SSRS must be installed and running during the MBAM Server installation.<br>Configure SSRS in "native" mode and not in unconfigured or "SharePoint" mode. |
| SSRS instance rights - required for configuring Reports only if you're installing databases on a separate server from the server where Reports are configured. | Required instance rights:<br>- Create Folders<br>- Publish Reports |
| Windows PowerShell 3.0 or later | Windows PowerShell doesn't have to be installed on this Database server if you're using Windows PowerShell to configure the database from a remote computer. |

## <a href="" id="bkmk-prereqsams"></a>Prerequisites for the Administration and Monitoring Server

The following sections list the installation prerequisites for the MBAM Administration and Monitoring Server.

### Windows Server web server role

This role must be added to a server operating system that is supported for the Administration and Monitoring Server feature.

### Web server (IIS) management tools

Select **IIS Management Scripts and Tools**.

### SSL certificate

Optional. To secure communication between the client computers and the web services, you must obtain and install a certificate that a trusted security authority signed.

### Web server role services

#### Common HTTP Features

- Static Content
- Default Document

#### Application Development

- ASP.NET
- .NET Extensibility
- ISAPI Extensions
- ISAPI Filters

#### Security

- Windows Authentication
- Request Filtering

### Windows Server features

#### .NET Framework 4.5 features

- .NET Framework 4.5 or 4.6
  - **Windows Server 2016** - .NET Framework 4.6 is already installed for these versions of Windows Server, but you must enable it.
  - **Windows Server 2012 or Windows Server 2012 R2** - .NET Framework 4.5 is already installed for these versions of Windows Server, but you must enable it.
  - **Windows Server 2008 R2** - .NET Framework 4.5 isn't included with Windows Server 2008 R2, so you must [download Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653) and install it separately.

- WCF Activation
  - HTTP Activation
  - Non-HTTP Activation (Only for Windows Server 2008, 2012, and 2012 R2)

- TCP Activation

#### Windows Process Activation Service

- Process Model
- .NET Framework Environment
- Configuration APIs

### ASP.NET MVC 4.0

[ASP.NET MVC 4 download](/aspnet/mvc/mvc4)

> [!NOTE]
> ASP.NET MVC 4.0 is no longer required after the January 2023 servicing update (HF08).

### Service principal name (SPN)

The web applications require an SPN for the virtual host name under the domain account that you use for the web application pools.

If your administrative rights permit you to create SPNs in Active Directory Domain Services, MBAM creates the SPN for you. See [Setspn](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11)) for information about the rights required to create SPNs.

If you don't have administrative rights to create SPNs, you must ask the Active Directory administrators in your organization to create the SPN for you by using the following command:

`Setspn -s http/mbamvirtual contoso\mbamapppooluser`

`Setspn -s http/mbamvirtual.contoso.com contoso\mbamapppooluser`

In the code example, the virtual host name is `mbamvirtual.contoso.com`, and the domain account used for the web application pools is `contoso\mbamapppooluser`.

> [!NOTE]
> If you set up load balancing, use the same application pool account on all servers.

For more information about registering SPNs for fully qualified, NetBIOS, and custom host names, see [Planning how to secure the MBAM websites](planning-how-to-secure-the-mbam-websites.md).

## Prerequisites for the Self-Service Portal

### Supported version of Windows Server

For the list of supported versions, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).

### ASP.NET MVC 4.0

[ASP.NET MVC 4 download](/aspnet/mvc/mvc4)

> [!NOTE]
> ASP.NET MVC 4.0 is no longer required after the January 2023 servicing update (HF08).

### Web Service IIS Management Tools

Select **IIS Management Scripts and Tools**.

### Service principal name (SPN)

The web applications require an SPN for the virtual host name under the domain account that you use for the web application pools.

If your administrative rights permit you to create SPNs in Active Directory Domain Services, MBAM creates the SPN for you. See [Setspn](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11)) for information about the rights required to create SPNs.

If you don't have administrative rights to create SPNs, you must ask the Active Directory administrators in your organization to create the SPN for you by using the following command:

`Setspn -s http/mbamvirtual contoso\mbamapppooluser`

`Setspn -s http/mbamvirtual.contoso.com contoso\mbamapppooluser`

In the code example, the virtual host name is `mbamvirtual.contoso.com`, and the domain account used for the web application pools is `contoso\mbamapppooluser`.

> [!NOTE]
> If you set up load balancing, use the same application pool account on all servers.

For more information about registering SPNs for fully qualified, NetBIOS, and custom host names, see [Planning how to secure the MBAM websites](planning-how-to-secure-the-mbam-websites.md).

## Prerequisites for the Management Workstation

Before you install the MBAM client, [download the MBAM group policy templates](../solutions/how-to-download-and-deploy-mdop-group-policy--admx--templates.md). Configure them with the settings that you want to implement in your environment for BitLocker Drive Encryption.

Before you install the MBAM Client, also do the following steps:

- [Copy the MBAM 2.5 group policy templates](copying-the-mbam-25-group-policy-templates.md)
- [Edit the MBAM 2.5 group policy settings](editing-the-mbam-25-group-policy-settings.md)

## Related articles

[Preparing your environment for MBAM 2.5](preparing-your-environment-for-mbam-25.md)

[Planning to deploy MBAM 2.5](planning-to-deploy-mbam-25.md)

[MBAM 2.5 supported configurations](mbam-25-supported-configurations.md)
