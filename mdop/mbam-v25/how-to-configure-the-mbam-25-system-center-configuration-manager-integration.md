---
title: How to configure the MBAM 2.5 System Center Configuration Manager integration
description: This article explains how to configure Microsoft BitLocker Administration and Monitoring (MBAM) to use the System Center Configuration Manager integration topology, which integrates MBAM with Configuration Manager.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to configure the MBAM 2.5 System Center Configuration Manager integration

This article explains how to configure Microsoft BitLocker Administration and Monitoring (MBAM) to use the System Center Configuration Manager integration topology, which integrates MBAM with Configuration Manager.

The instructions explain how to configure Configuration Manager integration by using:

- A Windows PowerShell cmdlet.

- The MBAM Server Configuration wizard.

The instructions are based on the recommended architecture in [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md).

## Before you start the configuration

- Review the recommended architecture for MBAM. For more information, see [High-level architecture of MBAM 2.5 with Configuration Manager integration topology](high-level-architecture-of-mbam-25-with-configuration-manager-integration-topology.md).
- Review the supported configurations for MBAM. For more information, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).
- Complete the required prerequisites on each server. For more information, see:
  - [MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md)
  - [MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology](mbam-25-server-prerequisites-that-apply-only-to-the-configuration-manager-integration-topology.md)
- Install the MBAM server software on each server where you'll configure an MBAM Server feature. For this topology, you must install the Configuration Manager console on the computer where you're installing the MBAM server software. For more information, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).
- Review Windows PowerShell prerequisites. This task is applicable only if you're going to use Windows PowerShell cmdlets to configure MBAM. For more information, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md).

## To configure Configuration Manager integration by using Windows PowerShell

1.  Before you start the configuration, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md) to review the prerequisites for using Windows PowerShell.

2.  Use the **Enable-MbamCMIntegration** Windows PowerShell cmdlet to configure the Reports. To get information about this cmdlet, type **Get-Help Enable-MbamCMIntegration**.

## To configure the System Center Configuration Manager integration by using the wizard

1.  On the server where you want to configure the System Center Configuration Manager Integration feature, start the MBAM Server Configuration wizard. You can select **MBAM Server Configuration** from the **Start** menu to open the wizard.

2.  Select **Add New Features**, select **System Center Configuration Manager Integration**, and then select **Next**.

    The wizard checks that the server meets all prerequisites for the Configuration Manager integration.

3.  If the prerequisite check is successful, select **Next** to continue. Otherwise, resolve any missing prerequisites, and then select **Check prerequisites again**.

4.  Use the following descriptions to enter the field values in the wizard:

    | Field | Description |
    |--|--|
    | SQL Server Reporting Services server | Fully qualified domain name (FQDN) of the server with the Reporting Service point role. This is the server to which the MBAM Configuration Manager Reports are deployed. If you don't specify a server, the Configuration Manager reports are deployed to the local server. |
    | SQL Server Reporting Services instance | Name of the SQL Server Reporting Services (SSRS) instance where the Configuration Manager Reports are deployed. If you don't specify an instance, the Configuration Manager reports are deployed to the default SSRS instance name. The value you enter is ignored if the server has System Center 2012 Configuration Manager installed. |

5.  On the **Summary** page, review the features that will be added.

    > [!NOTE]
    > To create a Windows PowerShell script of the entries you just made, select **Export PowerShell Script**, and save the script.

6.  Select **Add** to add the Configuration Manager Integration feature to the server, and then select **Close**.

## Related articles

[Configuring the MBAM 2.5 server features](configuring-the-mbam-25-server-features.md)

[Validating the MBAM 2.5 server feature configuration](validating-the-mbam-25-server-feature-configuration.md)
