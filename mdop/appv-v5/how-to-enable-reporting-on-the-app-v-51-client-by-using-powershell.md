---
title: How to enable reporting on the App-V 5.1 client by using Windows PowerShell
description: Use the following procedure to configure the App-V 5.1 for reporting.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---


# How to enable reporting on the App-V 5.1 client by using Windows PowerShell

Use the following procedure to configure the App-V 5.1 for reporting.

## To configure the computer running the App-V 5.1 client for reporting

1. Install the App-V 5.1 client. For more information about installing the client see [How to Deploy the App-V Client](how-to-deploy-the-app-v-client-51gb18030.md).

2. After you have installed the App-V 5.1 client, use the **Set-AppvClientConfiguration** PowerShell to configure appropriate Reporting Configuration settings:

    | Setting | Description |
    |--|--|
    | ReportingEnabled | Enables the client to return information to a reporting server. This setting is required for the client to collect the reporting data on the client. |
    | ReportingServerURL | Specifies the location on the reporting server where client information is saved. For example, `http://<reportingservername>:<reportingportnumber>`. <br> **Note:** This is the port number that was assigned during the Reporting Server setup. |
    | Reporting Start Time | This is set to schedule the client to automatically send the data to the server. This setting will indicate the hour at which the reporting data will start to send. It is in the 24 hour format and will take a number between 0-23. |
    | ReportingRandomDelay | Specifies the maximum delay (in minutes) for data to be sent to the reporting server. When the scheduled task is started, the client generates a random delay between 0 and ReportingRandomDelay and will wait the specified duration before sending data. |
    | ReportingInterval | Specifies the retry interval that the client will use to resend data to the reporting server. |
    | ReportingDataCacheLimit | Specifies the maximum size in megabytes (MB) of the XML cache for storing reporting information. The size applies to the cache in memory. When the limit is reached, the log file will roll over. |
    | ReportingDataBlockSize | Specifies the maximum size in megabytes (MB) of the XML cache for storing reporting information. The size applies to the cache in memory. When the limit is reached, the log file will roll over. |

3. After the appropriate settings have been configured, the computer running the App-V 5.1 client will automatically collect data and will send the data back to the reporting server.

   Additionally, administrators can manually send the data back in an on-demand manner using the **Send-AppvClientReport** PowerShell cmdlet.

## Related topics

[Administering App-V 5.1 by Using PowerShell](administering-app-v-51-by-using-powershell.md)
