---
title: How to configure the MBAM 2.5 reports
description: This article explains two methods to configure the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 reports feature.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to configure the MBAM 2.5 reports

This article explains how to configure the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 reports feature by using:

- A Windows PowerShell cmdlet.

- The MBAM Server Configuration wizard.

The instructions are based on the recommended architecture in [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md).

## Before you start the configuration

- Review the recommended architecture for MBAM. For more information, see [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md).
- Review the supported configurations for MBAM. For more information, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).
- Complete the required prerequisites on each server. For more information, see:
  - [MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md)
  - [MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology](mbam-25-server-prerequisites-that-apply-only-to-the-configuration-manager-integration-topology.md) (if applicable)
- Install the MBAM Server software on each server where you plan to configure an MBAM server feature. For more information, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).
- Review the prerequisites for using Windows PowerShell if you plan to use Windows PowerShell cmdlets to configure MBAM server features. For more information, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md).

## To configure the reports by using Windows PowerShell

1.  Before you start the configuration, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md) to review the prerequisites for using Windows PowerShell.

2.  Use the **Enable-MbamReport** Windows PowerShell cmdlet to configure the Reports. To get information about this Windows PowerShell cmdlet, type **Get-Help Enable-MbamReport**.

## To configure the reports by using the wizard

1. On the server where you want to configure the Reports, start the **MBAM Server Configuration** wizard. You can select **MBAM Server Configuration** from the **Start** menu to open the wizard.

2. Select **Add New Features**, select **Reports**, and then select **Next**. The wizard checks that the server meets all prerequisites for the reports.

3. Select **Next** to continue.

4. Using the following descriptions, enter the field values in the wizard:

    | Field | Description |
    |--|--|
    | SQL Server Reporting Services instance | Instance of SQL Server Reporting Services where the reports will be configured. |
    | Reporting role domain group | Name of the domain Users group whose members have rights to access the reports on the Administration and Monitoring Server. |
    | SQL Server name | Name of the server where the Compliance and Audit Database is configured. |
    | SQL Server database instance | Name of the instance of SQL Server (for example, *MSSQLSERVER*) where the Compliance and Audit Database is configured. **Note:** You must add an exception on the Reports computer to enable inbound traffic on the port of the Reporting Server (the default port is 80). |
    | Database name | Name of the Compliance and Audit Database. By default, the database name is **MBAM Compliance Status**, although you can change the name when you configure the Compliance and Audit Database. **Note:** If you're upgrading from a previous version of MBAM, you must use the same database name as the name used in your previous deployment. |
    | Compliance and Audit Database domain account | Domain user account and password to access the Compliance and Audit Database. If the value you enter in the **Read-only access domain user or group** field on the **Configure Databases** page is a user, you must enter that same value in this field. If the value that you enter in the **Read-only access domain user or group** field on the **Configure Databases** page is a group, the value that you enter in this field must be a member of that group. Configure the password for this account to never expire. The user account should be able to access all data that is available to the MBAM Reports Users group. |

5. When you finish your entries, select **Next**.

    The wizard checks that the server meets all prerequisites for the reports feature.

6. Select **Next** to continue.

7. On the **Summary** page, review the features that will be added.

    > [!NOTE]
    > To create a Windows PowerShell script of the entries that you just made, click **Export PowerShell Script**, and then save the script.

8. Select **Add** to add the Reports on the server, and then select **Close**.

## Related articles

[Server event logs](server-event-logs.md)

[Configuring the MBAM 2.5 server features](configuring-the-mbam-25-server-features.md)

[How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md)

[Validating the MBAM 2.5 server feature configuration](validating-the-mbam-25-server-feature-configuration.md)
