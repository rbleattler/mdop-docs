---
title: How to configure the MBAM 2.5 databases
description: This article explains two methods to configure the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 Compliance and Audit Database and the Recovery Database.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to configure the MBAM 2.5 databases

This article explains how to configure the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 Compliance and Audit Database and the Recovery Database by using:

- A Windows PowerShell cmdlet.

- The MBAM Server Configuration wizard.

The instructions are based on the recommended architecture in [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md).

## Before you start the configuration

- Review the recommended architecture for MBAM. For more information, see [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md).
- Review the supported configurations for MBAM. For more information, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).
- Complete the required prerequisites on each server. For more information, see:
  - [MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md)
  - [MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology](mbam-25-server-prerequisites-that-apply-only-to-the-configuration-manager-integration-topology.md) (if applicable)
- Install the MBAM Server software on each server where you plan to configure an MBAM Server feature. For more information, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).

  > [!NOTE]
  > You can install the databases to a remote SQL Server computer by using Windows PowerShell or an exported data-tier application (DAC) package. For more information about DAC packages, see [Data-tier applications (DAC)](/sql/relational-databases/data-tier-applications/data-tier-applications).

- Review the prerequisites for using Windows PowerShell if you plan to use Windows PowerShell cmdlets to configure MBAM Server features. For more information, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md).

## To configure the databases by using Windows PowerShell

1.  Before you start the configuration, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md) to review the prerequisites for using Windows PowerShell.

2.  Use the **Enable-MbamDatabase** Windows PowerShell cmdlet to configure the databases. To get information about this Windows PowerShell cmdlet, type **Get-Help Enable-MbamDatabase**.

## To configure the Compliance and Audit Database by using the wizard

1. On the server where you want to configure the databases, start the **MBAM Server Configuration** wizard. You can select **MBAM Server Configuration** from the **Start** menu to open the wizard.

2. Select **Add New Features**, select **Compliance and Audit Database** and **Recovery Database**, and then select **Next**. The wizard checks that the server meets all prerequisites for the databases.

3. If the prerequisite check is successful, select **Next** to continue. Otherwise, resolve any missing prerequisites, and then select **Check prerequisites again**.

4. Using the following descriptions, enter the field values in the wizard:

    | Field | Description |
    |--|--|
    | SQL Server name | Name of the server where you're configuring the Compliance and Audit Database. **Note:** You must add an exception on the Compliance and Audit Database computer to enable inbound traffic on the Microsoft SQL Server port. The default port number is 1433. |
    | SQL Server database instance | Name of the database instance where the compliance and audit data will be stored. You must also specify where the database information will be located. |
    | Database name | Name of the database that will store the compliance data. **Note:** If you're upgrading from a previous version of MBAM, you must use the same database name as the name that was used in your previous deployment. |
    | Read/write access domain user or group | Domain user or group that has read/write permission to this database to enable the web applications to access the data and reports in this database. If you enter a user in this field, it must be the same value as the value in the **Web service application pool domain account** field on the **Configure Web Applications** page. If you enter a group in this field, the value in the **Web service application pool domain account** field on the **Configure Web Applications** page must be a member of the group you enter in this field. |
    | Read-only access domain user or group | Name of the user or group that has read-only permission to this database to enable the reports to access the compliance data in this database. If you enter a user in this field, it must be the same user as the one you specify in the **Compliance and Audit Database domain account** field on the **Configure Reports** page. If you enter a group in this field, the value that you specify in the **Compliance and Audit Database domain account** field on the **Configure Reports** page must be a member of the |

5. Continue to the next section to configure the Recovery Database.

## To configure the Recovery Database by using the wizard

1. Using the following descriptions, enter the field values in the wizard:

    | Field | Description |
    |--|--|
    | **SQL Server name** | Name of the server where you're configuring the Recovery Database. **Note:** You must add an exception on the Recovery Database computer to enable inbound traffic on the Microsoft SQL Server port. The default port number is 1433. |
    | **SQL Server database instance** | Name of the database instance where the recovery data will be stored. You must also specify where the database information will be located. |
    | **Database name** | Name of the database that will store the recovery data. **Note:** If you're upgrading from a previous version of MBAM, you must use the same database name as the name that was used in your previous deployment. |
    | **Read/write access domain user or group** | Domain user or group that has read/write permission to this database to enable the web applications to access the data and reports in this database. If you enter a user in this field, it must be the same value as the value in the **Web service application pool domain account** field on the **Configure Web Applications** page. If you enter a group in this field, the value in the **Web service application pool domain account** field on the **Configure Web Applications** page must be a member of the group you enter in this field. |

2. When you finish your entries, select **Next**.

    The wizard checks that the server meets all prerequisites for the databases.

3. If the prerequisite check is successful, select **Next** to continue. Otherwise, resolve any missing prerequisites, and then select **Next** again.

4. On the **Summary** page, review the features that will be added.

    > [!NOTE]
    > To create a Windows PowerShell script of the entries that you just made, click **Export PowerShell Script**, and then save the script.

5. Select **Add** to add the MBAM databases on the server, and then select **Close**.

## Related articles

[Server event logs](server-event-logs.md)

[Configuring the MBAM 2.5 server features](configuring-the-mbam-25-server-features.md)

[How to configure the MBAM 2.5 reports](how-to-configure-the-mbam-25-reports.md)

[How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md)

[Validating the MBAM 2.5 server feature configuration](validating-the-mbam-25-server-feature-configuration.md)
