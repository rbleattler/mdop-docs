---
title: How to transfer access and configurations to another version of a package by using the App-V 5.1 management console
description: Use the following procedure to transfer the access and default package configurations to another version of a package by using the App-V 5.1 management console.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to transfer access and configurations to another version of a package by using the App-V 5.1 management console

Use the following procedure to transfer the access and default package configurations to another version of a package by using the management console.

## To transfer access and configurations to another version of a package

1.  To view the package that you want to configure, open the App-V 5.1 Management Console. Select the package to which you will transfer the new configuration, right-click the package and select **transfer default configuration from** or **transfer access and configurations from**, depending on the configuration that you want to transfer.

2.  To transfer the configuration, in the **Select Previous Version** dialog box, select the package that contains the settings that you want to transfer, and then click **OK**.

    If you select **transfer default configuration from**, then only the underlying dynamic deployment configuration will be transferred.

    If you select **transfer access and configurations from**, then all access permissions, as well as the configuration settings, will be copied.

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)
