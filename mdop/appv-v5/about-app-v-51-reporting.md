---
title: About App-V 5.1 reporting
description: Microsoft Application Virtualization (App-V) 5.1 includes a built-in reporting feature that helps you collect information about computers running the App-V 5.1 client and information about virtual application package usage.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# About App-V 5.1 reporting

Microsoft Application Virtualization (App-V) 5.1 includes a built-in reporting feature that helps you collect information about computers running the App-V 5.1 client and information about virtual application package usage. You can use this information to generate reports from a centralized database.

## <a href="" id="---------app-v-5-1-reporting-overview"></a> App-V 5.1 Reporting Overview

The following list displays the end-to-end high-level workflow for reporting in App-V 5.1.

1. The App-V 5.1 Reporting server has the following prerequisites:

    - Internet Information Service (IIS) web server role

    - Windows Authentication role (under **IIS / Security**)

    - SQL Server installed and running with SQL Server Reporting Services (SSRS)

    To confirm SQL Server Reporting Services is running, view `http://localhost/Reports` in a web browser as administrator on the server that will host App-V 5.1 Reporting. The SQL Server Reporting Services Home page should display.

2. Install the App-V 5.1 reporting server and associated database. For more information about installing the reporting server, see [How to install the Reporting Server on a Standalone Computer and Connect it to the Database](how-to-install-the-reporting-server-on-a-standalone-computer-and-connect-it-to-the-database51.md). Configure the time when the computer running the App-V 5.1 client should send data to the reporting server.

3. If you aren't using an electronic software distribution system such as Configuration Manager to view reports, then you can define reports in SQL Server Reporting Service.

    > [!NOTE]
    > If you are using the Configuration Manager integration with App-V 5.1, most reports are generated from Configuration Manager rather than from App-V 5.1.

4. After importing the App-V 5.1 PowerShell module using `Import-Module AppvClient` as administrator, enable the App-V 5.1 client. This sample PowerShell cmdlet enables App-V 5.1 reporting:

    ```powershell
    Set-AppvClientConfiguration -reportingserverurl <url>:<port> -reportingenabled 1 - ReportingStartTime <0-23> - ReportingRandomDelay <#min>
    ```

    To immediately send App-V 5.1 report data, run `Send-AppvClientReport` on the App-V 5.1 client.

    For more information about installing the App-V 5.1 client with reporting enabled, see [About Client Configuration Settings](about-client-configuration-settings51.md). To administer App-V 5.1 Reporting with Windows PowerShell, see [How to Enable Reporting on the App-V 5.1 Client by Using PowerShell](how-to-enable-reporting-on-the-app-v-51-client-by-using-powershell.md).

5. After the reporting server receives the data from the App-V 5.1 client, it sends the data to the reporting database. When the database receives and processes the client data, a successful reply is sent to the reporting server, and then a notification is sent to the App-V 5.1 client.

6. When the App-V 5.1 client receives the success notification, it empties the data cache to conserve space.

    > [!NOTE]
    > By default the cache is cleared after the server confirms receipt of data. You can manually configure the client to save the data cache.

If the App-V 5.1 client device doesn't receive a success notification from the server, it retains data in the cache and tries to resend data at the next configured interval. Clients continue to collect data and add it to the cache.

### <a href="" id="-------------app-v-5-1-reporting-server-frequently-asked-questions"></a> App-V 5.1 reporting server frequently asked questions

The following table displays answers to common questions about App-V 5.1 reporting

| Question | More Information |
|--|--|
| What is the frequency that reporting information is sent to the reporting database? | The frequency depends on how the reporting task is configured on the computer running the App-V 5.1 client. You must configure the frequency / interval for sending the reporting data. App-V 5.1 Reporting isn't enabled by default. |
| What information is stored in the reporting server database? | The following list displays what is stored in the reporting database: <ul><li>The operating system running on the computer running the App-V 5.1 client: host name, version, service pack, type - client/server, processor architecture.</li><li>App-V 5.1 Client information: version.</li><li>Published package list: GUID, version GUID, name.</li><li>Application usage information: name, version, streaming server, user (domain\alias), package version GUID, launch status and time, shutdown time.</li></ul> |
| What is the average volume of information that is sent to the reporting server? | It depends. The following list displays the three sets of the data sent to the reporting server: <ol><li>Operating system, and App-V 5.1 client information. ~150 Bytes, every time this data is sent.</li><li>Published package list. ~7 KB for 30 packages. This is sent only when the package list is updated with a publishing refresh, which is done infrequently; if there's no change, this information isn't sent.</li><li>Virtual application usage information - about 0.25 KB per event. Opening and closing count as one event if both occur before sending the information. When sending using a scheduled task, only the data since the last successful upload is sent to the server. If sending manually through the PowerShell cmdlet, there's an optional argument that controls if the data needs to be resent next time around - that argument is **DeleteOnSuccess**.</li><li>So for example, if 20 applications are opened and closed and reporting information is scheduled to be sent daily, the typical daily traffic should be about 0.15 KB + 20 x 0.25 KB, or about 5 KB/user</li></ol> |
| Can reporting be scheduled? | Yes. Besides manually sending reporting using PowerShell Cmdlets (**Send-AppvClientReport**), the task can be scheduled so it happens automatically. There are two ways to schedule the reporting: <ol><li>Using PowerShell cmdlets - **Set-AppvClientConfiguration**. For example: <br>`Set-AppvClientConfiguration -ReportingEnabled 1 -ReportingServerURL http://any.com/appv-reporting`<br>For a complete list of client configuration settings, see [About Client Configuration Settings](about-client-configuration-settings51.md) and look for the following entries: **ReportingEnabled**, **ReportingServerURL**, **ReportingDataCacheLimit**, **ReportingDataBlockSize**, **ReportingStartTime**, **ReportingRandomDelay**, **ReportingInterval**.</li><li>By using Group Policy. If distributed using the domain controller, the settings are the same as previously listed.<br>**Note**<br>Group Policy settings override local settings configured using PowerShell.</li></ol> |

## <a href="" id="---------app-v-5-1-client-reporting"></a> App-V 5.1 Client Reporting

To use App-V 5.1 reporting, you must install and configure the App-V 5.1 client. After the client installs, use the **Set-AppVClientConfiguration** PowerShell cmdlet or the **ADMX Template** to configure reporting. The reporting feature cmdlets are available by using the following link and are prefaced by **Reporting**. For a complete list of client configuration settings, see [About Client Configuration Settings](about-client-configuration-settings51.md). The following section provides examples of App-V 5.1 client reporting configuration using PowerShell.

### Configuring App-V Client reporting using PowerShell

The following examples show how PowerShell parameters can configure the reporting features of the App-V 5.1 client.

> [!NOTE]
> The following configuration task can also be configured using Group Policy settings in the App-V 5.1 ADMX template. For more information about using the ADMX template, see [How to Modify App-V 5.1 Client Configuration Using the ADMX Template and Group Policy](how-to-modify-app-v-51-client-configuration-using-the-admx-template-and-group-policy.md).

**To enable reporting and to initiate data collection on the computer running the App-V 5.1 client**:

```powershell
Set-AppVClientConfiguration -ReportingEnabled 1
```

**To configure the client to automatically send data to a specific reporting server**:

```powershell
Set-AppVClientConfiguration -ReportingServerURL http://MyReportingServer:MyPort/ -ReportingStartTime 20 -ReportingInterval 1 -ReportingRandomDelay 30 -ReportingInterval 1 -ReportingRandomDelay 30
```

This example configures the client to automatically send the reporting data to the reporting server URL **http://MyReportingServer:MyPort/**. Additionally, the reporting data is sent daily between 8:00 and 8:30 PM, depending on the random delay generated for the session.

**To limit the size of the data cache on the client**:

```powershell
Set-AppvClientConfiguration -ReportingDataCacheLimit 100
```

Configures the maximum size of the reporting cache on the computer running the App-V 5.1 client to 100 MB. If the cache limit is reached before the data is sent to the server, then the log rolls over and data is overwritten as necessary.

**To configure the data block size transmitted across the network between the client and the server**:

```powershell
Set-AppvClientConfiguration -ReportingDataBlockSize 10240
```

Specifies the maximum data block that the client sends to 10,240 MB.

### Types of data collected

The following table displays the types of information you can collect by using App-V 5.1 reporting.

|Client Information  |Package Information  |Application Usage  |
|---------|---------|---------|
|Host Name |Package Name|Start and End Times|
|App-V 5.1 Client Version |Package Version|Run Status|
|Processor Architecture |Package Source|Shutdown State|
|Operating System Version|Percent Cached|Application Name|
|Service Pack Level| |Application Version|
|Operating System Type| |Username|
| | |Connection Group|

The client collects and saves this data in an **.xml** format. The data cache is hidden by default and requires administrator rights to open the XML file.

### Sending data to the server

You can configure the computer that is running the App-V 5.1 client to automatically send data to the specified reporting server. To specify the server, use the **Set-AppvClientConfiguration** cmdlet with the following settings:

- ReportingEnabled
- ReportingServerURL
- ReportingStartTime
- ReportingInterval
- ReportingRandomDelay

After you configure the previous settings, you must create a scheduled task. The scheduled task contacts the server specified by the **ReportingServerURL** setting and starts the transfer. If you want to manually send data outside of the scheduled times, use the following PowerShell cmdlet:

```powershell
Send-AppVClientReport -URL http://MyReportingServer:MyPort/ -DeleteOnSuccess
```

If you previously configured the reporting server, then you can omit the **-URL** parameter. Alternatively, if the data should be sent to an alternate location, specify a different URL to override the configured **ReportingServerURL** for this data collection.

The **-DeleteOnSuccess** parameter indicates that if the transfer is successful, then the data cache is cleared. If this isn't specified, then the cache isn't cleared.

### Manual Data Collection

You can also use the **Send-AppVClientReport** cmdlet to manually collect data. This solution is helpful with or without an existing reporting server. The following list displays information about collecting data with or without a reporting server.

| With a Reporting Server | Without a Reporting Server |
|--|--|
| If you have an existing App-V 5.1 reporting Server, create a customized scheduled task or script. Specify that the client send the data to the specified location with the desired frequency. | If you don't have an existing App-V 5.1 reporting Server, use the **-URL** parameter to send the data to a specified share. For example: <br> `Send-AppVClientReport -URL \Myshare\MyData\ -DeleteOnSuccess` <br> The previous example sends the reporting data to **\MyShare\MyData** location indicated by the **-URL** parameter. After the data is sent, the cache is cleared. <br> **Note** <br> If a location other than the Reporting Server is specified, the data is sent using **.xml** format with no more processing. |

### Creating Reports

To retrieve report information and create reports using App-V 5.1, you must use one of the following methods:

- **Microsoft SQL Server Reporting Services (SSRS)** - Microsoft SQL Server Reporting Services is available with Microsoft SQL Server. SSRS isn't installed when you install the App-V 5.1 reporting server. It must be deployed separately to generate the associated reports.

    Use the following link for more information about using [Microsoft SQL Server Reporting Services](/previous-versions/sql/sql-server-2008-r2/ms159106(v=sql.105)).

- **Scripting** - You can generate reports by scripting directly against the App-V 5.1 reporting database. For example:

    **Stored Procedure:**

    **spProcessClientReport** is scheduled to run at midnight or 12:00 AM.

    To run the Microsoft SQL Server Scheduled Stored procedure, the Microsoft SQL Server Agent must be running. You should ensure that the Microsoft SQL Server Agent is set to **AutoStart**. For more information, see [Auto restart SQL Server Agent](/sql/ssms/agent/autorestart-sql-server-agent-sql-server-management-studio).

    The stored procedure is also created when using the App-V 5.1 database scripts.

You should also ensure that the reporting server web service's **Maximum Concurrent Connections** is set to a value that the server can manage without impacting availability. The recommended number of **Maximum Concurrent Connections** for the **Reporting Web Service** is **10,000**.

## Related articles

[Deploying the App-V 5.1 Server](deploying-the-app-v-51-server.md)

[How to install the Reporting Server on a Standalone Computer and Connect it to the Database](how-to-install-the-reporting-server-on-a-standalone-computer-and-connect-it-to-the-database51.md)
