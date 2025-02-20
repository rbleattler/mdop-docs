---
title: How to move the MBAM 2.5 reports
description: Use these procedures to move the reports feature from one computer to another.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to move the MBAM 2.5 reports

Use these procedures to move the reports feature from one computer to another. For example, to move the reports feature from Server A to Server B.

The high-level steps for moving the Reports feature are:

1.  Stop all instances of the MBAM Administration and Monitoring Website.

2.  Install the MBAM 2.5 Server software on Server B and configure the Reports feature on Server B.

3.  Update the reports connection data on the MBAM Administration and Monitoring servers.

4.  Resume the instance of the MBAM Administration and Monitoring Website.

> [!NOTE]
> To run the example Windows PowerShell scripts in this topic, you must update the Windows PowerShell execution policy to enable scripts to be run. For more information, see [Getting started with PowerShell](/powershell/scripting/learn/ps101/01-getting-started#execution-policy).

## Stop the MBAM Administration and Monitoring website

-   On the server that is running the Administration and Monitoring Website, use the Internet Information Services (IIS) Manager console to stop the Administration and Monitoring Website.

    To automate this procedure, you can use Windows PowerShell to enter a command that's similar to the following command:

    ```powershell
    Stop-Website "Microsoft BitLocker Administration and Monitoring"
    ```

## Install MBAM Server software and run the MBAM Server Configuration wizard on Server B

1.  Install the MBAM Server software on Server B. For instructions, see [Installing the MBAM 2.5 Server Software](installing-the-mbam-25-server-software.md).

2.  On Server B, start the MBAM Server Configuration wizard, select **Add New Features**, and then select only the **Reports** feature.

    Alternatively, you can use the **Enable-MbamReport** Windows PowerShell cmdlet to configure the Reports.

    For instructions on how to configure the Reports, see [How to Configure the MBAM 2.5 Reports](how-to-configure-the-mbam-25-reports.md).

## Update the reports connection data on the Administration and Monitoring Server

1.  On the server that is running the Reports feature, use the Internet Information Services (IIS) Manager console to update the Reports URL.

2.  Expand **Microsoft BitLocker Administration and Monitoring**, and then select the **HelpDesk** node.

3.  In the **Management** section of the **Features View**, select **Configuration Editor**.

4.  In the **Section** field, select **appSettings**.

5.  Select the **Collection** row, and then select the "ellipses" button (`...`) at the far right of the pane to open the **Collection Editor**.

6.  In the **Collection Editor**, select the row that contains **Microsoft.Mbam.Reports.Url**, and update the value for **Microsoft.Mbam.Reports.Url** to reflect the server name for Server B.

    If you previously configured the Reports feature on a named instance of SQL Server Reporting Services, add or update the name of the instance to the URL, for example:

    `http://$SERVERNAME$/ReportServer_$SQLSRSINSTANCENAME$/Pages....)`

7.  To automate this procedure, you can use Windows PowerShell to run a command on the Administration and Monitoring Server that is similar to the following code example.

    ```powershell
    Set-WebConfigurationProperty '/appSettings/add[@key="Microsoft.Mbam.Reports.Url"]' -PSPath "IIS:\\sites\Microsoft Bitlocker Administration and Monitoring\HelpDesk" -Name "Value" -Value "http://$SERVERNAME$/ReportServer[_$SRSINSTANCENAME$]/Pages/ReportViewer.aspx?/Microsoft+BitLocker+Administration+and+Monitoring/"
    ```

    Using the descriptions in the following table, replace the values in the code example with values that match your environment.

    | Parameter         | Description                                                        |
    |-------------------|--------------------------------------------------------------------|
    | `$SERVERNAME$`    | Name of the server to which the Reports were moved.                |
    | `$SRSINSTANCENAME$` | Name of the instance of SQL Server Reporting Services to which the Reports were moved. |

## Resume the instance of the Administration and Monitoring Website

1.  On the server that is running the Administration and Monitoring Website, use the Internet Information Services (IIS) Manager console to start the Administration and Monitoring Website.

2.  To automate this procedure, you can use Windows PowerShell to run a command that is similar to the following command:

    ``` powershell
    Start-Website "Microsoft BitLocker Administration and Monitoring"
    ```

    > [!NOTE]
    > To run this command, you must add the IIS module for Windows PowerShell to the current instance of Windows PowerShell.

## Related articles

[How to configure the MBAM 2.5 reports](how-to-configure-the-mbam-25-reports.md)

[Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md)

[Moving MBAM 2.5 features to another server](moving-mbam-25-features-to-another-server.md)
