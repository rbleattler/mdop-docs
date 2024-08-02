---
title: Using the App-V 5.1 client management console
description: This article provides information about how you can configure and manage the Microsoft Application Virtualization (App-V) 5.1 client management console.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Using the App-V 5.1 client management console

This article provides information about how you can configure and manage the Microsoft Application Virtualization (App-V) 5.1 client management console.

## Modify App-V 5.1 client configuration

The App-V 5.1 client has settings that you can configure to determine how the client runs in your environment. You can manage these settings on the computer that runs the client or by using Windows PowerShell or Group Policy. For more information about how to modify the client using PowerShell or group policy configuration, see [How to modify client configuration by using Windows PowerShell](how-to-modify-client-configuration-by-using-powershell51.md).

## <a href="" id="the-app-v-5-1-client-management-console-"></a>The App-V 5.1 client management console

You can obtain information about the App-V 5.1 client or perform specific tasks by using the App-V 5.1 client management console. Many of the tasks that you can perform in the client management console you can also perform by using PowerShell. The associated PowerShell cmdlets for each action are also displayed in the following table. For more information about how to use PowerShell, see [Administering App-V 5.1 by Using PowerShell](administering-app-v-51-by-using-powershell.md).

The client management console contains the following described main tabs.

### Overview

The **Overview** tab contains the following elements:

- **Update**: Use the **Update** tile to refresh a virtualized application or to receive a new virtualized package. The **Last Refresh** displays the current version of the virtualized package.
- **Download all virtual applications**: Use the **Download** tile to download all of the packages provisioned to the current user. The associated PowerShell cmdlet is **Mount-AppvClientPackage**.
- **Work Offline**: Use this tile to disallow all automatic and manual virtual application updates. The associated PowerShell cmdlet is **Set-AppvPublishServer -UserRefreshEnabled -GlobalRefreshEnabled**.

### Virtual Apps

The **VIRTUAL APPS** tab displays all of the packages that are published to the user. You can also select a specific package and see all of the applications that are part of that package. This displays information about packages that are currently in use and how much of each package is downloaded to the computer. You can also start and stop package downloads. Additionally, you can repair the user state. A repair deletes all user data that is associated with a package.

### App Connection Groups

The **APP CONNECTION GROUPS** tab displays all of the connection groups that are available to the current user. Select a specific connection group to see all of the packages that are part of the selected group. This displays information about connection groups that are already in use and how much of the connection group contents are downloaded to the computer. Additionally, you can start and stop connection group downloads. You can use this section to initiate a repair. A repair removes all of the user state that is associated with a connection group.

The associated PowerShell cmdlets:

- Download: **Mount-AppvClientConnectionGroup**
- Repair: **AppvClientConnectionGroup**

## Related articles

[How to access the client management console](how-to-access-the-client-management-console51.md)

[How to configure the client to receive package and connection groups updates from the publishing server](how-to-configure-the-client-to-receive-package-and-connection-groups-updates-from-the-publishing-server-51.md)

[Operations for App-V 5.1](operations-for-app-v-51.md)
