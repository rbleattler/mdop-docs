---
title: App-V 5.1 Supported Configurations
description: This article specifies the requirements to install and run Microsoft Application Virtualization (App-V) 5.1 in your environment.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/02/2020
---

# App-V 5.1 Supported Configurations

>Applies to: Windows 10, version 1607; Window Server 2019; Windows Server 2016; Windows Server 2012 R2; Windows Server 2012; Windows Server 2008 R2 (Extended Security Update)

This article specifies the requirements to install and run Microsoft Application Virtualization (App-V) 5.1 in your environment.

## App-V Server system requirements

This section lists the operating system and hardware requirements for all of the App-V Server components.

### Unsupported App-V 5.1 Server scenarios

The App-V 5.1 Server doesn't support the following scenarios:

- Deployment to a computer that runs Microsoft Windows Server Core.

- Deployment to a computer that runs a previous version of App-V 5.1 Server components. You can install App-V 5.1 side by side with the App-V 4.5 Lightweight Streaming Server (LWS) server only. Deployment of App-V side by side with the App-V 4.5 Application Virtualization Management Service (HWS) server isn't supported.

- Deployment to a computer that runs Microsoft SQL Server Express edition.

- Deployment to a domain controller.

- Short paths. If you plan to use a short path, you must create a new volume.

### Management server operating system requirements

The following table lists the operating systems that are supported for the App-V 5.1 Management server installation.

> [!NOTE]
> Microsoft provides support for the current service pack and, in some cases, the immediately preceding service pack. To find the support timelines for your product, see the [Microsoft Lifecycle Policy](/lifecycle/).

 | Operating System       | Service Pack | System Architecture |
|----------------------------------|--------------|---------------------|
| Microsoft Windows Server 2019  |      |    64-bit   |
| Microsoft Windows Server 2016  |      |    64-bit   |
| Microsoft Windows Server 2012 R2 |      |    64-bit   |
| Microsoft Windows Server 2012  |      |    64-bit   |
| Microsoft Windows Server 2008 R2 [Extended Security Update](https://www.microsoft.com/windows-server/extended-security-updates)|  SP1   |    64-bit   |

> [!IMPORTANT]
> Deployment of the Management server role to a computer with Remote Desktop Sharing (RDS) enabled is not supported.

### <a href="" id="management-server-hardware-requirements-"></a>Management server hardware requirements

- Processor: 1.4 GHz or faster, 64-bit (x64) processor

- RAM: 1 GB RAM (64-bit)

- Disk space: 200 MB available hard disk space, not including the content directory

### Management server database requirements

The following table lists the SQL Server versions that are supported for the App-V 5.1 Management database installation.

| SQL Server version          | Service pack | System architecture |
|-----------------------------|--------------|---------------------|
| Microsoft SQL Server 2019   |              | 32-bit or 64-bit    |
| Microsoft SQL Server 2017   |              | 32-bit or 64-bit    |
| Microsoft SQL Server 2016   | SP2          | 32-bit or 64-bit    |
| Microsoft SQL Server 2014   | SP2          | 32-bit or 64-bit    |
| Microsoft SQL Server 2012   | SP2          | 32-bit or 64-bit    |
| Microsoft SQL Server 2008 R2| SP3          | 32-bit or 64-bit    |

For more information on user configuration files with SQL server 2016 or later, see [App-V Server publishing might fail when you apply user configuration files with SQL Server 2016 or later](https://support.microsoft.com/topic/app-v-server-publishing-might-fail-when-you-apply-user-configuration-files-with-sql-server-2016-or-later-e1b69d83-3c42-3ac2-13a8-340cac2bd3bb).

### Publishing server operating system requirements

The following table lists the operating systems that are supported for the App-V 5.1 Publishing server installation.

| Operating System       | Service Pack | System Architecture |
|----------------------------------|--------------|---------------------|
| Microsoft Windows Server 2019  |      |    64-bit   |
| Microsoft Windows Server 2016  |      |    64-bit   |
| Microsoft Windows Server 2012 R2 |      |    64-bit   |
| Microsoft Windows Server 2012  |      |    64-bit   |
| Microsoft Windows Server 2008 R2 [Extended Security Update](https://www.microsoft.com/windows-server/extended-security-updates) |  SP1   |    64-bit   |

### <a href="" id="publishing-server-hardware-requirements-"></a>Publishing server hardware requirements

App-V adds no other requirements beyond those of Windows Server.

- Processor: 1.4 GHz or faster, 64-bit (x64) processor

- RAM: 2 GB RAM (64-bit)

- Disk space: 200 MB available hard disk space, not including the content directory

### Reporting server operating system requirements

The following table lists the operating systems that are supported for the App-V 5.1 Reporting server installation.

| Operating System       | Service Pack | System Architecture |
|----------------------------------|--------------|---------------------|
| Microsoft Windows Server 2019  |      |    64-bit   |
| Microsoft Windows Server 2016  |      |    64-bit   |
| Microsoft Windows Server 2012 R2 |      |    64-bit   |
| Microsoft Windows Server 2012  |      |    64-bit   |
| Microsoft Windows Server 2008 R2 [Extended Security Update](https://www.microsoft.com/windows-server/extended-security-updates) |  SP1   |    64-bit   |

### <a href="" id="reporting-server-hardware-requirements-"></a>Reporting server hardware requirements

App-V adds no other requirements beyond those of Windows Server.

- Processor: 1.4 GHz or faster, 64-bit (x64) processor

- RAM: 2 GB RAM (64-bit)

- Disk space: 200 MB available hard disk space

### Reporting server database requirements

The following table lists the SQL Server versions that are supported for the App-V 5.1 Reporting database installation.

| SQL Server version     | Service Pack  | System Architecture     |
|------------------------------|---------------|-------------------------------|
| Microsoft SQL Server 2019  |  CU4  |    32-bit or 64-bit   |
| Microsoft SQL Server 2017  |     |    32-bit or 64-bit   |
| Microsoft SQL Server 2016  |  SP2  |    32-bit or 64-bit   |
| Microsoft SQL Server 2014  |     |    32-bit or 64-bit   |
| Microsoft SQL Server 2012  |  SP2  |    32-bit or 64-bit   |
| Microsoft SQL Server 2008 R2 |  SP3  |    32-bit or 64-bit   |

## <a href="" id="bkmk-client-supp-cfgs"></a>App-V client system requirements

The following table lists the operating systems that are supported for the App-V 5.1 client installation.

> [!NOTE]
> With the Windows 10 Anniversary release (aka 1607 version), the App-V client is in-box and will block installation of any previous version of the App-V client

| Operating system                          | Service pack | System architecture |
|-------------------------------------------|--------------|---------------------|
| Microsoft Windows 10 (pre-1607 version)   |              | 32-bit or 64-bit    |
| Microsoft Windows 8.1                     |              | 32-bit or 64-bit    |
| Windows 7                                 | SP1          | 32-bit or 64-bit    |

The following App-V client installation scenarios aren't supported, except as noted:

- Computers that run Windows Server

- Computers that run App-V 4.6 SP1 or earlier versions

- The App-V 5.1 Remote Desktop services client is supported only for RDS-enabled servers

### <a href="" id="app-v-client-hardware-requirements-"></a>App-V client hardware requirements

The following list displays the supported hardware configuration for the App-V 5.1 client installation.

- Processor: 1.4 GHz or faster 32-bit (x86) or 64-bit (x64) processor

- RAM: 1 GB (32-bit) or 2 GB (64-bit)

- Disk: 100 MB for installation, not including the disk space that is used by virtualized applications.

## Remote Desktop Services client system requirements


The following table lists the operating systems that are supported for App-V 5.1 Remote Desktop Services (RDS) client installation.

| Operating System       | Service Pack | System Architecture |
|----------------------------------|--------------|---------------------|
| Microsoft Windows Server 2019  |      |    64-bit   |
| Microsoft Windows Server 2016  |      |    64-bit   |
| Microsoft Windows Server 2012 R2 |      |    64-bit   |
| Microsoft Windows Server 2012  |      |    64-bit   |
| Microsoft Windows Server 2008 R2 [Extended Security Update](https://www.microsoft.com/windows-server/extended-security-updates) |  SP1   |    64-bit   |

### Remote Desktop Services client hardware requirements

App-V adds no other requirements beyond those of Windows Server.

- Processor: 1.4 GHz or faster, 64-bit (x64) processor

- RAM: 2 GB RAM (64-bit)

- Disk space: 200 MB available hard disk space

## Sequencer system requirements

The following table lists the operating systems that are supported for the App-V 5.1 Sequencer installation.

| Operating System       | Service Pack | System Architecture |
|----------------------------------|--------------|---------------------|
| Microsoft Windows Server 2019  |      |    64-bit   |
| Microsoft Windows Server 2016  |      |    64-bit   |
| Microsoft Windows Server 2012 R2 |      |    64-bit   |
| Microsoft Windows Server 2012  |      |    64-bit   |
| Microsoft Windows Server 2008 R2 [Extended Security Update](https://www.microsoft.com/windows-server/extended-security-updates) |  SP1   |    64-bit   |
| Microsoft Windows 10     |      | 32-bit and 64-bit |
| Microsoft Windows 8.1    |      | 32-bit and 64-bit |
| Microsoft Windows 7      |  SP1   | 32-bit and 64-bit |

### Sequencer hardware requirements

See the Windows or Windows Server documentation for the hardware requirements. App-V adds no other hardware requirements.

## <a href="" id="bkmk-supp-ver-sccm"></a>Supported versions of System Center Configuration Manager

The App-V client supports the following versions of System Center Configuration Manager:

- Microsoft System Center 2012 Configuration Manager

- System Center 2012 R2 Configuration Manager

- System Center 2012 R2 Configuration Manager SP1

The following App-V and System Center Configuration Manager version matrix shows all officially supported combinations of App-V and Configuration Manager.

> [!NOTE]
> Both App-V 4.5 and 4.6 have exited Mainstream support.

| App-V Version | System Center Configuration Manager 2007 | System Center 2012 Configuration Manager | System Center 2012 Configuration Manager SP1 | System Center 2012 R2 Configuration Manager | System Center 2012 R2 Configuration Manager SP1 | System Center 2012 Configuration Manager SP2 | System Center Configuration Manager Version 1511 |
|--|--|--|--|--|--|--|--|
| App-V 5.0 SP3 | MSI-Wrapper Only | No | 2012 SP1 CU4 | 2012 R2 CU1 | Yes | Yes | Yes |
| App-V 5.1 | MSI-Wrapper Only | No | 2012 SP1 CU4 | 2012 R2 CU1 | Yes | Yes | Yes |

For more information about how Configuration Manager integrates with App-V, see [Planning for App-V Integration with Configuration Manager](/previous-versions/system-center/system-center-2012-R2/jj822982(v=technet.10)).

## Related articles

[App-V 5.1 Prerequisites](app-v-51-prerequisites.md)
