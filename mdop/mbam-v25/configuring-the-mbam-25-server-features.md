---
title: Configuring the MBAM 2.5 server features
description: Use this information as a starting place for configuring Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 server features after installing the MBAM 2.5 server software.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Configuring the MBAM 2.5 server features

Use this information as a starting place for configuring Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 server features after [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md). There are two methods you can use to configure MBAM:

- MBAM Server Configuration wizard

- Windows PowerShell cmdlets

## Before you start configuring MBAM server features

Review and complete the following steps before you start configuring the MBAM server features:

- Review the recommended architecture for MBAM. For more information, see [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md).
- Review the supported configurations for MBAM. For more information, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).
- Complete the required prerequisites on each server. For more information, see:
  - [MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md)
  - [MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology](mbam-25-server-prerequisites-that-apply-only-to-the-configuration-manager-integration-topology.md)
- Install the MBAM server software on each server where you'll configure an MBAM server feature. For more information, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).
- Review the prerequisites for using Windows PowerShell to configure MBAM server features, if you're using this method to configure MBAM server features. For more information, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md).

## Steps for configuring MBAM server features

The following list describes the features that you need to configure on a separate server, according to the recommended [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md).

- Configure the databases. For more information, see [How to configure the MBAM 2.5 databases](how-to-configure-the-mbam-25-databases.md).
- Configure the reports. For more information, see [How to configure the MBAM 2.5 reports](how-to-configure-the-mbam-25-reports.md).
- Configure the web applications. For more information, see [How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md).
- Configure the System Center Configuration Manager integration (if applicable). For more information, see [How to configure the MBAM 2.5 System Center Configuration Manager integration](how-to-configure-the-mbam-25-system-center-configuration-manager-integration.md).

For a list of events about MBAM server feature configuration, see [Server event logs](server-event-logs.md).

## Related articles

[Configuring the MBAM 2.5 server Features](configuring-the-mbam-25-server-features.md)