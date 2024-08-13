---
title: Evaluating MBAM 2.5 in a test environment
description: This article describes how you can set up a test environment to evaluate Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 in the stand-alone or System Center Configuration Manager integration topology.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Evaluating MBAM 2.5 in a test environment

This article describes how you can set up a test environment to evaluate Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 in the stand-alone or System Center Configuration Manager integration topology.

## Evaluating MBAM 2.5 by using the stand-alone topology

To evaluate MBAM by using the stand-alone topology, use the information in the following tables to install the MBAM server software, and then configure the MBAM server features in your test environment.

### To evaluate MBAM 2.5 by using the stand-alone topology

1. Before installing MBAM, do the following:

    - Ensure that you have installed all of the prerequisite software. For more information, see [MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md).
    - Check the required hardware, RAM, and other specifications. For more information, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).
    - Review the prerequisites for using Windows PowerShell if you plan to use the cmdlets to configure MBAM. For more information, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md).

2. Install the MBAM server software, and then configure the features you want.

    - Install the MBAM server software on each server where you want to configure an MBAM server feature. For more information, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).
    - Configure the Compliance and Audit Database and the Recovery Database. For more information, see [How to configure the MBAM 2.5 databases](how-to-configure-the-mbam-25-databases.md).
    - Configure the Reports feature. For more information, see [How to configure the MBAM 2.5 reports](how-to-configure-the-mbam-25-reports.md).
    - Configure the web applications. For more information, see [How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md).

3. On a client computer, do the following:

   1.  Install the MBAM client on a client computer.

   2.  Apply the MBAM Group Policy Objects (GPOs) to the computer.

   3.  Set the following registry keys to force the MBAM client to wake up faster and at regular intervals:

       ``` syntax
       [HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\FVE\MDOPBitLockerManagement
       "ClientWakeupFrequency"=dword:00000001
       "StatusReportingFrequency"=dword:00000001
       ```

       ``` syntax
       [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MBAM]
       "NoStartupDelay"=dword:00000001
       ```

       > [!NOTE]
       > Because these keys wake up the MBAM client every minute, we recommend that you use these registry key settings only in a test environment.

   4.  Restart the **BitLocker Management Client Service**.

## Evaluating MBAM 2.5 by using the System Center 2012 Configuration Manager integration topology

To evaluate MBAM by using the Configuration Manager Integration topology, use the information in the following tables to install the MBAM server software, and then configure the MBAM server features in your test environment. After installing the MBAM client on a client computer, you will complete additional steps to force the MBAM client to report the computer's status to MBAM more quickly.

### To evaluate MBAM 2.5 by using the System Center 2012 Configuration Manager integration topology

1. Before installing MBAM, review the prerequisite software and supported configuration.

    - Ensure that you have installed all of the prerequisite software. For more information, see the following articles:
      - [MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md)
      - [MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology](mbam-25-server-prerequisites-that-apply-only-to-the-configuration-manager-integration-topology.md)
    - Check the required hardware, RAM, and other specifications. For more information, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).
    - Review the prerequisites for using Windows PowerShell if you plan to use the cmdlets to configure MBAM. For more information, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md).
    - Create or edit the .mof files. For more information, see the following articles:
      - [Edit the configuration.mof file](edit-the-configurationmof-file-mbam-25.md)
      - [Create or edit the sms_def.mof file](create-or-edit-the-sms-defmof-file-mbam-25.md)

2. Install the MBAM server software, and then configure the features you want.

    - Install the MBAM server software on each server where you want to configure an MBAM server feature. For more information, see [Installing the MBAM 2.5 Server Software](installing-the-mbam-25-server-software.md)

      > [!NOTE]
      > You can install the databases to a remote SQL Server computer by using Windows PowerShell or an exported data-tier application (DAC) package. For more information about DAC packages, see [Data-tier applications (DAC)](/sql/relational-databases/data-tier-applications/data-tier-applications).

    - Configure the Compliance and Audit Database and the Recovery Database. For more information, see [How to configure the MBAM 2.5 databases](how-to-configure-the-mbam-25-databases.md).
    - Configure the Reports feature. For more information, see [How to configure the MBAM 2.5 reports](how-to-configure-the-mbam-25-reports.md).
    - Configure the web applications. For more information, see [How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md).
    - Configure the System Center Configuration Manager to install the Configuration Manager objects. For more information, see [How to configure the MBAM 2.5 System Center Configuration Manager integration](how-to-configure-the-mbam-25-system-center-configuration-manager-integration.md).

3. On a client computer, do the following:

   1.  Install the MBAM client and the Configuration Manager Client on a client computer.

   2.  Apply the MBAM Group Policy Objects to the computer.

   3.  Set the following registry keys to force the MBAM client to wake up faster and at regular intervals:

       ``` syntax
       [HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\FVE\MDOPBitLockerManagement
       "ClientWakeupFrequency"=dword:00000001
       "StatusReportingFrequency"=dword:00000001
       ```

       ``` syntax
       [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MBAM]
       "NoStartupDelay"=dword:00000001
       ```

       > [!NOTE]
       > Because these keys wake up the MBAM client every minute, we recommend that you use these registry key settings only in a test environment.

   4.  Restart the **BitLocker Management Client Service**.

   5.  In Control Panel, open **Configuration Manager**, and then click the **Actions** tab.

   6.  Select **Hardware Inventory Cycle**, and then click **Run Now**. This step runs the hardware inventory by using the new classes that you imported to your .mof files, and then sends the data to the Configuration Manager server.

   7.  Select **Machine Policy Retrieval & Evaluation Cycle**, and then click **Run Now** to apply the Group Policy Objects that are relevant to that client computer.

4. In the Configuration Manager console, do the following:

   1.  In the navigation pane, right-click **MBAM Supported Computers**, click **Update Membership**, and then click **Yes** to force the client computer to report its membership immediately.

   2.  In the navigation pane, click **MBAM Supported Computers** to verify that the client computer appears in the collection.

5. On the client computer, in Control Panel, reopen **Configuration Manager** again, and do the following:

   1.  Click the **Actions** tab, and then rerun **Machine Policy Retrieval & Evaluation Cycle**.

   2.  Click the **Configurations** tab, select the BitLocker baseline, and then click **Evaluate**.

6. In the Configuration Manager console, verify that the client computer appears on the Enterprise Compliance Report: as follows:

   1.  In the navigation pane, select the **Monitoring** workspace.

   2.  In the console tree, expand **Overview** &gt; **Reporting** &gt; **Reports** &gt; **MBAM**.

   3.  Select the folder that represents the language in which you want to view reports, and then select the report in the results pane.

## Evaluating MBAM 2.5 by using the System Center Configuration Manager 2007 integration topology

To evaluate MBAM by using the Configuration Manager Integration topology, follow the same steps to install and configure MBAM in your test environment as you use in a production environment. After installing the MBAM client on a client computer, complete the additional steps in this topic to enable the MBAM client to start reporting the computer's status to MBAM more quickly.

### To evaluate MBAM by using the Configuration Manager 2007 integration topology

1. Before you install MBAM, do the following tasks:

    - Ensure that you have installed all of the prerequisite software. For more information, see the following articles:
      - [MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md)
      - [MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology](mbam-25-server-prerequisites-that-apply-only-to-the-configuration-manager-integration-topology.md)

    - Check the required hardware, RAM, and other specifications. For more information, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).

    - Create or edit the .mof files. For more information, see the following articles:
      - [Edit the configuration.mof file](edit-the-configurationmof-file-mbam-25.md)
      - [Create or edit the sms_def.mof file](create-or-edit-the-sms-defmof-file-mbam-25.md)

2. Install the MBAM server software, and then configure the features you want.

    - Install the MBAM server software on each server where you want to configure an MBAM server feature. For more information, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).

        > [!NOTE]
        > You can install the databases to a remote SQL Server computer by using Windows PowerShell or an exported data-tier application (DAC) package. For more information about DAC packages, see [Data-tier applications (DAC)](/sql/relational-databases/data-tier-applications/data-tier-applications).

    - Configure the Compliance and Audit Database and the Recovery Database. For more information, see [How to configure the MBAM 2.5 databases](how-to-configure-the-mbam-25-databases.md).

    - Configure the Reports feature. For more information, see [How to configure the MBAM 2.5 reports](how-to-configure-the-mbam-25-reports.md).

    - Configure the web applications. For more information, see [How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md).

    - Configure the System Center Configuration Manager to install the Configuration Manager objects. For more information, see [How to configure the MBAM 2.5 System Center Configuration Manager integration](how-to-configure-the-mbam-25-system-center-configuration-manager-integration.md).

3. On a client computer, do the following:

   1.  Install the MBAM client on a client computer.

   2.  Apply the MBAM Group Policy Objects to the computer.

   3.  Set the following registry keys to force the MBAM client to wake up more quickly and at faster intervals:

       ``` syntax
       [HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\FVE\MDOPBitLockerManagement
       "ClientWakeupFrequency"=dword:00000001
       "StatusReportingFrequency"=dword:00000001
       ```

       ``` syntax
       [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MBAM]
       "NoStartupDelay"=dword:00000001
       ```

       > [!NOTE]
       > Because these keys wake up the MBAM client every minute, we recommend that you use these registry key settings only in an evaluation environment.

   4.  Restart the **BitLocker Management Client Service**.

   5.  In Control Panel, open **Configuration Manager**, and then click the **Actions** tab.

   6.  Select **Machine Policy Retrieval & Evaluation Cycle**, and then click **Run Now** to apply the Group Policy Objects that are relevant to that client computer.

   7.  Select **Hardware Inventory Cycle**, and then click **Run Now**. This step runs the hardware inventory by using the new classes that you imported to your .mof files and then sends the data to the Configuration Manager server.

4. In the Configuration Manager console, do the following:

   1.  In the navigation pane, right-click **MBAM Supported Computers**, click **Update Membership**, and then click **Yes** to force the client computer to report its membership immediately.

   2.  In the navigation pane, click **MBAM Supported Computers** to verify that the client computer appears in the collection.

5. On the client computer, in Control Panel, reopen **Configuration Manager** again, and do the following:

   1.  Click the **Actions** tab, and then rerun **Machine Policy Retrieval & Evaluation Cycle**.

   2.  Click the **Configurations** tab, select the BitLocker baseline, and click **Evaluate**.

6. In the Configuration Manager console, verify that the client computer appears on the Enterprise Compliance Report, as follows

   1.  In the navigation pane, expand **Computer Management** &gt; **Reporting** &gt; **Reporting Services** &gt; **&lt;server name&gt;MBAM**.

   2.  Within the **MBAM** node, select the folder that represents the language in which you want to view reports, and then select the report from the results pane.

## Related articles

[About MBAM 2.5 SP1](about-mbam-25-sp1.md)
