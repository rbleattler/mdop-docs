---
title: Illustrated features of an MBAM 2.5 deployment
description: This article describes the individual features that make up a Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 deployment for the MBAM stand-alone and Configuration Manager integration topologies.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/15/2018
---

# Illustrated features of an MBAM 2.5 deployment

This article describes the individual features that make up a Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 deployment for the following topologies:

- MBAM Stand-alone

- System Center Configuration Manager Integration

> [!IMPORTANT]
> These features don't represent the recommended architecture for deploying MBAM. Use this information only as a guide to understand the individual features that make up an MBAM deployment. for the recommended architecture for MBAM, see [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md).

For a list of the supported versions of the software mentioned in this article, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).

## <a href="" id="bkmk-standalone"></a> MBAM stand-alone topology

The following image and table explain the features in an MBAM stand-alone topology.

![Conceptual diagram of the stand-alone server features.](images/mbam2-5-standalonecomponents.png)

|Feature type|Description|Database|
|-|-|-|
|Recovery Database|This database stores recovery data that is collected from MBAM client computers.|This feature is configured on a server running Windows Server and a supported SQL Server instance.|
|Compliance and Audit Database|This database stores compliance data, which is used primarily for the Reports that SQL Server Reporting Services hosts.|This feature is configured on a server running Windows Server and a supported SQL Server instance.|
|Compliance and Audit Reports|||
|Reporting Web Service|This web service enables communication between the Administration and Monitoring Website and the SQL Server instance where reporting data is stored.|This feature is installed on a server running Windows Server.|
|Reporting Website (Administration and Monitoring Website)|You view Reports from the Administration and Monitoring Website. The Reports provide recovery audit and compliance status data about the client computers in your enterprise.|This feature is configured on a server running Windows Server.|
|SQL Server Reporting Services (SSRS)|Reports are configured in an SSRS database instance. Reports can be viewed directly from SSRS or from the Administration and Monitoring Website.|This feature is configured on a server running Windows Server and a supported SQL Server instance that is running SSRS.|
|Self-Service Server|||
|Self-Service Web Service|This web service is used by the MBAM Client and the Administration and Monitoring Website and Self-Service Portal to communicate to the Recovery Database.|This feature is installed on a computer running Windows Server.|
|Self-Service Website (Self-Service Portal)|This website enables end users on client computers to independently sign in to a website to get a recovery key if they lose or forget their BitLocker password.|This feature is configured on a computer running Windows Server.|
|Administration and Monitoring Server|||
|Administration and Monitoring Web Service|The Monitoring Web Service is used by the MBAM Client and the websites to communicate to the databases.|This feature is installed on a computer running Windows Server.|

> [!IMPORTANT]
> The Self-Service Web Service is no longer available in Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 SP1, in which the MBAM Client, the Administration and Monitoring Website, and the Self-Service Portal communicate directly with the Recovery Database.

> [!WARNING]
> The Monitoring Web Service is no longer available in Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 SP1 since the MBAM Client and the websites communicate directly with the Recovery Database.

## <a href="" id="bkmk-cmintegrated"></a>System Center Configuration Manager integration topology

The following image and table explain the features in the System Center Configuration Manager integration topology.

![Conceptual diagram of the Configuration Manager server features.](images/mbam2-5-cmcomponents.png)

> [!IMPORTANT]
> The Self-Service Web Service is no longer available in Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 SP1, in which the MBAM Client, the Administration and Monitoring Website, and the Self-Service Portal communicate directly with the Recovery Database.

> [!WARNING]
> The Monitoring Web Service is no longer available in Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 SP1 since the MBAM Client and the websites communicate directly with the Recovery Database.

| Feature type | Description |
|--|--|
| Self-Service Server |  |
| Self-Service Web Service | This web service is used by the MBAM Client and the Self-Service Portal to communicate to the Recovery Database. |
| Self-Service Website | This website enables end users on client computers to independently sign in to a website to get a recovery key if they lose or forget their BitLocker password. |
| Administration and Monitoring Server/Recovery Audit Report |  |
| Administration and Monitoring Web Service | This web service enables communication between the Administration and Monitoring Website and the SQL Server databases where reporting data is stored. |
| Administration and Monitoring Website | The Recovery Audit report is viewed from the Administration and Monitoring Website. Use the Configuration Manager console to view all other reports, or view reports directly from SQL Server Reporting Services. |
| Databases |  |
| Recovery Database | This database stores recovery data that is collected from MBAM client computers. |
| Audit Database | This database stores audit information about recovery attempts and activity. |
| Configuration Manager Features |  |
| Configuration Manager Management console | This console is built into Configuration Manager and is used to view reports. |
| Configuration Manager Reports | Reports show compliance and recovery audit data for client computers in your enterprise. |
| SQL Server Reporting Services | SSRS enables the MBAM Reports. Reports can be viewed directly from SSRS or from the Configuration Manager console. |

## Related articles

[High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md)

[About MBAM 2.5 SP1](about-mbam-25-sp1.md)
