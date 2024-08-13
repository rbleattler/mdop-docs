---
title: Prerequisites for the Configuration Manager integration feature
description: If you deploy MBAM with the System Center Configuration Manager integration topology, we recommend a three-server architecture
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Prerequisites for the Configuration Manager integration feature

If you deploy MBAM with the System Center Configuration Manager integration topology, we recommend a three-server architecture, as described in [High-level architecture of MBAM 2.5 with Configuration Manager integration topology](high-level-architecture-of-mbam-25-with-configuration-manager-integration-topology.md). This architecture can support 500,000 client computers.

## General prerequisites for the Configuration Manager integration feature

When you install MBAM with Configuration Manager, the following prerequisites are required in addition to the prerequisites for the stand-alone topology.

| Prerequisite | More information |
|--|--|
| The Configuration Manager Server is a primary site in the Configuration Manager system. | N/A |
| The Hardware Inventory Client Agent is on the Configuration Manager Server. | For System Center 2012 Configuration Manager, see [How to configure hardware inventory in Configuration Manager](/previous-versions/system-center/system-center-2012-R2/hh301103(v=technet.10)). |
| One of the following features are enabled, depending on the version of Configuration Manager that you use: <ul><li>Compliance Settings - (System Center 2012 Configuration Manager)</li><li>Desired Configuration Management (DCM) Client Agent - (Configuration Manager 2007)</li></ul> | For System Center 2012 Configuration Manager, see [Configuring compliance settings in Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg682002(v=technet.10)). |
| A reporting services point is defined in Configuration Manager. Required for SQL Server Reporting Services (SSRS). | For System Center 2012 Configuration Manager, see [Prerequisites for reporting in Configuration Manager](/previous-versions/system-center/system-center-2012-R2/hh338695(v=technet.10)). |
| Configuration Manager 2007 requires Microsoft .NET Framework 2.0 | The Desired Configuration Management (DCM) Client Agent in Configuration Manager 2007 requires .NET Framework 2.0 to report compliance. <br> **Note:** Installing .NET Framework 3.5 automatically installs .NET Framework 2.0. |

## Required permissions to install MBAM with Configuration Manager

To install MBAM with Configuration Manager, you must have an administrative user in Configuration Manager who has a security role with the minimum permissions listed in the following table. The table also shows the rights that you must have, beyond basic computer administrator rights, to install the MBAM Server.

### The permissions in the following table apply to both versions of Configuration Manager

| Permissions                                               | MBAM server feature                          |
|-----------------------------------------------------------|----------------------------------------------|
| SQL Server instance login server roles: - `dbcreator` - `processadmin` | - Recovery Database - Audit Database         |
| SSRS instance rights: - Create Folders - Publish Reports  | - System Center Configuration Manager Integration |

### System Center 2012 Configuration Manager

| Permissions                                                                 | Configuration Manager Server feature          |
|-----------------------------------------------------------------------------|----------------------------------------------|
| Configuration Manager site rights: - Read                                   | System Center Configuration Manager Integration |
| Configuration Manager collection rights: - Create - Delete - Read - Modify - Deploy Configuration Items | System Center Configuration Manager Integration |
| Configuration Manager configuration item rights: - Create - Delete - Read   | System Center Configuration Manager Integration |

### Configuration Manager 2007

| Permissions                                                                 | Configuration Manager Server feature          |
|-----------------------------------------------------------------------------|----------------------------------------------|
| Configuration Manager site rights: - Read                                   | System Center Configuration Manager Integration |
| Configuration Manager collection rights: - Create - Delete - Read - ReadResource | System Center Configuration Manager Integration |
| Configuration Manager configuration item rights: - Create - Delete - Read - Distribute | System Center Configuration Manager Integration |

## Required changes for the .mof files

To enable the client computers to report BitLocker compliance details through the MBAM Configuration Manager reports, you have to edit the Configuration.mof file and Sms\_def.mof file for System Center 2012 Configuration Manager and Microsoft System Center Configuration Manager 2007. For instructions, see [MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology](mbam-25-server-prerequisites-that-apply-only-to-the-configuration-manager-integration-topology.md).

## Related articles

[MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md)

[MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology](mbam-25-server-prerequisites-that-apply-only-to-the-configuration-manager-integration-topology.md)
