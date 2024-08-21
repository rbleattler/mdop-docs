---
title: Validating the MBAM 2.5 server feature configuration
description: When you finish the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 server feature deployment, we recommend that you validate the deployment to ensure that all features are successfully configured.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Validating the MBAM 2.5 server feature configuration

When you finish the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 server feature deployment, we recommend that you validate the deployment to ensure that all features are successfully configured. Use the procedure that matches the topology (stand-alone or System Center Configuration Manager integration) that you deployed.

## Validating the MBAM server deployment with the stand-alone topology

Use the following steps to validate your MBAM server deployment with the stand-alone topology.

### To validate a stand-alone MBAM server deployment

1.  On each server where an MBAM feature is deployed, select **Control Panel** &gt; **Programs** &gt; **Programs and Features**. Verify that **Microsoft BitLocker Administration and Monitoring** appears in the **Programs and Features** list.

    > [!NOTE]
    > To do the validation, you must use a domain account that has local computer administrative credentials on each server.

2.  On the server where the Recovery Database is configured, open SQL Server Management Studio and verify that the **MBAM Recovery and Hardware** database is configured.

3.  On the server where the Compliance and Audit Database is configured, open SQL Server Management Studio and verify that the **MBAM Compliance Status Database** is configured.

4.  On the server where the Reports feature is configured, open a web browser with administrative credentials and browse to the "Home" of the SQL Server Reporting Services site.

    The default Home location of a SQL Server Reporting Services site instance is at:

    `https://<MBAMReportsServerName>:<port>/Reports.aspx`

    To find the actual URL, use the Reporting Services Configuration Manager tool and select the instances that you specified during setup.

5.  Confirm that a reports folder named **Microsoft BitLocker Administration and Monitoring** contains a data source called **MaltaDataSource** and the language folders. The data source contains folders with names that represent languages (for example, en-us). The reports are in the language folders.

    > [!NOTE]
    > If you configure SQL Server Reporting Services (SSRS) as a named instance, the URL should resemble the following: `https://<MBAMReportsServerName>:<port>/Reports_<SSRSInstanceName>`

> [!NOTE]
> If SSRS wasn't configured to use Secure Socket Layer (SSL), when you install the MBAM server, the URL for the reports are set to HTTP instead of HTTPS. If you then go to the Administration and Monitoring website (also known as Help Desk) and select a report, the following message appears: "Only Secure Content is Displayed." To show the report, select **Show All Content**.

6. On the server where the Administration and Monitoring Website feature is configured, run **Server Manager**, browse to **Roles**, and then select **Web Server (IIS)** &gt; **Internet Information Services (IIS) Manager**.

7. In **Connections**, browse to *&lt;computer name&gt;* and select **Sites** &gt; **Microsoft BitLocker Administration and Monitoring**. Verify that the following are listed:

   - **MBAMAdministrationService**

   - **MBAMComplianceStatusService**

   - **MBAMRecoveryAndHardwareService**

8. On the server where the Administration and Monitoring website and Self-Service Portal are configured, open a web browser with administrative credentials.

9. Browse to the following websites to verify that they load successfully:

   - `https://<MBAMAdministrationServerName>:<port>/HelpDesk/` - confirm each of the links for navigation and reports

   - `https://<MBAMAdministrationServerName>:<port>/SelfService/`

   > [!NOTE]
   > It is assumed that you configured the server features on the default port without network encryption. If you configured the server features on a different port or virtual directory, change the URLs to include the appropriate port, for example:

   `https://<host name>:<port>/HelpDesk/`

   `https://<host name>:<port>/<virtualdirectory>/`

   If the server features were configured with network encryption, change `http://` to `https://`.

10. Browse to the following web services to verify that they load successfully. A page opens to indicate that the service is running, but the page doesn't display any metadata.

    - `https://<MBAMAdministrationServerName>:<port>/MBAMAdministrationService/AdministrationService.svc`

    - `https://<MBAMAdministrationServerName>:<port>/MBAMUserSupportService/UserSupportService.svc`

    - `https://<MBAMAdministrationServerName>:<port>/MBAMComplianceStatusService/StatusReportingService.svc`

    - `https://<MBAMAdministrationServerName>:<port>/MBAMRecoveryAndHardwareService/CoreService.svc`

## Validating the MBAM server deployment with the Configuration Manager integration topology

Use the following steps to validate your MBAM deployment with the Configuration Manager integration topology. Complete the validation steps that match the version of Configuration Manager that you use.

### <a href="" id="validating-the-mbam-server-deployment-with-system-center-2012-configuration-manager-"></a>Validating the MBAM server deployment with System Center 2012 Configuration Manager

Use these steps to validate your MBAM server deployment when you use MBAM with System Center 2012 Configuration Manager.

#### To validate a Configuration Manager integration MBAM server deployment - System Center 2012 Configuration Manager

1.  On the server where System Center 2012 Configuration Manager is deployed, open **Programs and Features** in **Control Panel**, and verify that **Microsoft BitLocker Administration and Monitoring** appears.

    > [!NOTE]
    > To validate the configuration, you must use a domain account that has local computer administrative credentials on each server.

2.  In the Configuration Manager console, select the **Assets and Compliance** workspace &gt; **Device Collections**, and confirm that a new collection called **MBAM Supported Computers** is displayed.

3.  In the Configuration Manager console, select the **Monitoring** workspace &gt; **Reporting** &gt; **Reports** &gt; **MBAM**.

4.  Verify that the **MBAM** folder contains subfolders, with names that represent different languages, and that the following reports are listed in each language subfolder:

    - BitLocker Computer Compliance

    - BitLocker Enterprise Compliance Dashboard

    - BitLocker Enterprise Compliance Details

    - BitLocker Enterprise Compliance Summary

5.  In the Configuration Manager console, select the **Assets and Compliance** workspace &gt; **Compliance Settings** &gt; **Configuration Baselines**, and confirm that the configuration baseline **BitLocker Protection** is listed.

6.  In the Configuration Manager console, select the **Assets and Compliance** workspace &gt; **Compliance Settings** &gt; **Configuration Items**, and confirm that the following new configuration items are displayed:

    - BitLocker Fixed Data Drives Protection

    - BitLocker Operating System Drive Protection

### Validating the MBAM server deployment with Configuration Manager 2007

Use these steps to validate your MBAM server deployment when you use MBAM with Configuration Manager 2007.

#### To validate a Configuration Manager integration MBAM server deployment - Configuration Manager 2007

1.  On the server where Configuration Manager 2007 is deployed, open **Programs and Features** on **Control Panel** , and verify that **Microsoft BitLocker Administration and Monitoring** appears.

    > [!NOTE]
    > To validate the configuration, you must use a domain account that has local computer administrative credentials on each server.

2.  In the Configuration Manager console, select **Site Database &lt;SiteCode&gt; - &lt;ServerName&gt;, &lt;SiteName&gt;, Computer Management**, and confirm that a new collection called **MBAM Supported Computers** is displayed.

3.  In the Configuration Manager console, select **Reporting** &gt; **Reporting Services** &gt; **\\\\&lt;ServerName&gt;** &gt; **Report Folders** &gt; **MBAM**.

    Verify that the **MBAM** folder contains subfolders, with names that represent different languages, and that the following reports are listed in each language subfolder:

    - BitLocker Computer Compliance

    - BitLocker Enterprise Compliance Dashboard

    - BitLocker Enterprise Compliance Details

    - BitLocker Enterprise Compliance Summary

4.  In the Configuration Manager console, select **Desired Configuration Management** &gt; **Configuration Baselines**, and confirm that the configuration baseline **BitLocker Protection** is listed.

5.  In the Configuration Manager console, select **Desired Configuration Management** &gt; **Configuration Items**, and confirm that the following new configuration items are displayed:

    - BitLocker Fixed Data Drives Protection

    - BitLocker Operating System Drive Protection

## Related articles

[Configuring the MBAM 2.5 server features](configuring-the-mbam-25-server-features.md)
