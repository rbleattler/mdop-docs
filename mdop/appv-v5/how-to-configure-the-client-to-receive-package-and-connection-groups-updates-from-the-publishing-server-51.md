---
title: Configure the client to receive package and connection groups updates from the publishing server
description: Deploying packages and connection groups using the App-V 5.1 publishing server is helpful because it offers single-point management and high scalability.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Configure the client to receive package and connection groups updates from the publishing server

Deploying packages and connection groups using the App-V 5.1 publishing server is helpful because it offers single-point management and high scalability.

Use the following steps to configure the App-V 5.1 client to receive updates from the publishing server.

> [!NOTE]
> For the following procedures the management server was installed on a computer named **MyMgmtSrv**, and the publishing server was installed on a computer named **MyPubSrv**.

## To configure the App-V 5.1 client to receive updates from the publishing server

1.  Deploy the App-V 5.1 management and publishing servers, and add the required packages and connection groups. For more information about adding packages and connection groups, see [How to Add or Upgrade Packages by Using the Management Console](how-to-add-or-upgrade-packages-by-using-the-management-console-51-gb18030.md) and [How to Create a Connection Group](how-to-create-a-connection-group51.md).

2.  To open the management console click the following link, open a browser and go to the following URL: `http://MyMgmtSrv/AppvManagement/Console.html`. Then import, publish, and entitle all the packages and connection groups which will be necessary for a particular set of users.

3.  On the computer running the App-V 5.1 client, open an elevated PowerShell command prompt, run the following command:

    ```powershell
    Add-AppvPublishingServer -Name ABC -URL http://MyPubSrv/AppvPublishing
    ```

    This command will configure the specified publishing server. You should see output similar to the following:

    ```output
    Id                        : 1

    SetByGroupPolicy          : False

    Name                      : ABC

    URL                       : http:// MyPubSrv/AppvPublishing

    GlobalRefreshEnabled      : False

    GlobalRefreshOnLogon      : False

    GlobalRefreshInterval     : 0

    GlobalRefreshIntervalUnit : Day

    UserRefreshEnabled        : True

    UserRefreshOnLogon        : True

    UserRefreshInterval       : 0

    UserRefreshIntervalUnit   : Day
    ```

    The returned Id in this case is `1`.

4.  On the computer running the App-V 5.1 client, open a PowerShell command prompt, and type the following command:

    ```powershell
    Sync-AppvPublishingServer  -ServerId  1**
    ```

    The command will query the publishing server for the packages and connection groups that need to be added or removed for this particular client based on the entitlements for the packages and connection groups as configured on the management server.

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)
