---
title: Planning for MBAM 2.5 server deployment
description: This article lists the features that you deploy for the MBAM stand-alone and Configuration Manager topologies and lists the order in which you need to deploy them.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Planning for MBAM 2.5 server deployment

This article lists the features that you deploy for the MBAM stand-alone and Configuration Manager topologies and lists the order in which you need to deploy them. There's a recommended configuration for each topology. However, you can configure MBAM server databases and features in different configurations and across multiple servers, depending on your scalability requirements.

## Important planning considerations for both topologies

| Considerations | Details or purpose |
|--|--|
| Review the following before you start the deployment: <ul><li>[MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md)</li><li>[MBAM 2.5 supported configurations](mbam-25-supported-configurations.md)</li></ul> | Each MBAM feature has specific prerequisites that must be met before you start the MBAM installation. |
| BitLocker recovery keys in MBAM expire after a single use. | A single use means that the recovery key was retrieved through the Administration and Monitoring Website (also known as Help Desk), Self-Service Portal, or by using the **Get-MbamBitLockerRecoveryKey** Windows PowerShell cmdlet. |
| Keep track of the names of the computers on which you configure each feature. You'll use this information throughout the configuration process. | You might want to use the [MBAM 2.5 deployment checklist](mbam-25-deployment-checklist.md) for this purpose. |
| Configure only the group policy settings in the MDOP MBAM (BitLocker Management) node. Don't change the group policy settings in the BitLocker Drive Encryption node. | If you change the group policy settings in the BitLocker Drive Encryption node, MBAM won't work. |

## <a href="" id="planning-for-mbam-server-deployment---stand-alone-topology"></a>Planning for MBAM Server deployment - stand-alone topology

For the stand-alone topology, a two-server configuration is recommended for production environments, although configurations of three to four servers can be used.

The server infrastructure for the MBAM stand-alone topology contains the following features, which must be configured in the order listed:

1.  Databases: Compliance and Audit database, Recovery database

2.  Reports

3.  Web applications and their corresponding web services

    -   Administration and Monitoring Website

    -   Self-Service Portal

For a description of these features, see [High-level architecture of MBAM 2.5 with stand-alone topology](high-level-architecture-of-mbam-25-with-stand-alone-topology.md).

## <a href="" id="planning-for-mbam-server-deployment---configuration-manager-topology"></a>Planning for MBAM Server deployment - Configuration Manager topology


For the Configuration Manager Integration topology, a three-server configuration is recommended for production environments, although configurations of other servers can be used.

The Server infrastructure for the MBAM Configuration Manager topology contains the following features, which must be configured or performed in the order listed:

1.  Databases (Compliance and Audit Database and Recovery Database)

2.  Reports

3.  Web applications (and their corresponding web services)

    -   Administration and Monitoring Website

    -   Self-Service Portal

4.  System Center Configuration Manager Integration

For a description of these features, see [High-level architecture of MBAM 2.5 with Configuration Manager integration topology](high-level-architecture-of-mbam-25-with-configuration-manager-integration-topology.md).

## Related articles

[Planning to deploy MBAM 2.5](planning-to-deploy-mbam-25.md)

[Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md)
