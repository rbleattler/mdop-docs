---
title: High-level architecture of MBAM 2.5 with stand-alone topology
description: This article describes the recommended architecture for deploying Microsoft BitLocker Administration and Monitoring (MBAM) with the Configuration Manager stand-alone topology.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# High-level architecture of MBAM 2.5 with stand-alone topology

This article describes the recommended architecture for deploying Microsoft BitLocker Administration and Monitoring (MBAM) with the Configuration Manager stand-alone topology. In this topology, MBAM is deployed as a stand-alone product. You can alternatively deploy MBAM with the Configuration Manager Integration topology, which integrates MBAM with Configuration Manager. For more information, see [High-level architecture of MBAM 2.5 with Configuration Manager integration topology](high-level-architecture-of-mbam-25-with-configuration-manager-integration-topology.md).

For a list of the supported versions of the software mentioned in this article, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).

> [!NOTE]
> We recommend you use a single-server architecture in test environments only.

## Recommended number of servers and supported number of clients

The following table lists the recommended number of servers and supported number of clients in a production environment:

| Recommended architecture in a production environment | Details          |
|------------------------------------------------------|------------------|
| Number of servers and other computers                | Two servers<br>One workstation |
| Number of client computers supported                 | 500,000          |

## Recommended MBAM high-level architecture with the stand-alone topology

The following diagram and sections describe the recommended high-level, two-server architecture for MBAM with the stand-alone topology. MBAM multi-forest deployments require a one-way or two-way trust. One-way trusts require that the server domain trusts the client domain.

![Conceptual diagram of MBAM high-level architecture.](images/mbam2-5-2servers.png)

### Compliance and Audit Database

This feature is configured on a server running Windows Server and supported SQL Server instance. The **Compliance and Audit Database** stores compliance data, which is used primarily for reports that SQL Server Reporting Services hosts.

### Recovery Database

This feature is configured on a server running Windows Server and supported SQL Server instance. The **Recovery Database** stores recovery data that is collected from MBAM client computers.

### Reports

This feature is configured on a server running Windows Server and supported SQL Server instance. The **Reports** provide recovery audit and compliance status data about the client computers in your enterprise. You can access the reports from the Administration and Monitoring Website or directly from SQL Server Reporting Services.

### Administration and Monitoring Server

#### Administration and Monitoring website

This feature is configured on a computer running Windows Server. The **Administration and Monitoring Website** is used to:

- Help users regain access to their computers when they're locked out. This area of the website is commonly called the Help Desk.

- View reports that show compliance status and recovery activity for client computers.

#### Self-Service Portal

This feature is configured on a computer running Windows Server. The **Self-Service Portal** is a website that enables end users on client computers to independently sign in to a website to get a recovery key if they lose or forget their BitLocker password.

#### Monitoring web services for this website

This feature is configured on a computer running Windows Server. The **monitoring web services** are used by the MBAM client and the websites to communicate to the database.

> [!NOTE]
> The Monitoring Web Service is no longer available in Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 SP1 since the MBAM websites communicate directly with the Recovery Database.

### Management workstation

#### MBAM group policy templates

- The MBAM group policy templates are group policy settings that define implementation settings for MBAM, which enable you to manage BitLocker Drive Encryption.

- Before you run MBAM, you must download the group policy templates from [How to download and deploy MDOP group policy (.admx) templates](../solutions/how-to-download-and-deploy-mdop-group-policy--admx--templates.md) and copy them to a server or workstation that is running a supported Windows Server or Windows operating system.

- The workstation doesn't have to be a dedicated computer.

### MBAM client and Configuration Manager client computer

#### MBAM client software

The MBAM client:

- Uses group policy Objects to enforce BitLocker Drive Encryption on client computers in the enterprise.

- Collects the BitLocker recovery key for three data drive types: operating system drives, fixed data drives, and removable (USB) data drives.

- Collects recovery information and computer information about the client computers.

## Related articles

[About MBAM 2.5 SP1](about-mbam-25-sp1.md)

[High-level architecture of MBAM 2.5 with Configuration Manager integration topology](high-level-architecture-of-mbam-25-with-configuration-manager-integration-topology.md)

[Illustrated features of an MBAM 2.5 deployment](illustrated-features-of-an-mbam-25-deployment.md)
