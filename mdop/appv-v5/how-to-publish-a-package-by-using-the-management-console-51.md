---
title: Publish a package by using the management console
description: Use the following procedure to publish an App-V 5.1 package.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Publish a package by using the management console

Use the following procedure to publish an App-V 5.1 package. Once you publish a package, computers that are running the App-V 5.1 client can access and run the applications in that package.

> [!NOTE]
> The ability to enable only administrators to publish or unpublish packages (described below) is supported starting in App-V 5.0 SP3.

## To publish an App-V 5.1 package

1.  In the App-V 5.1 Management console. Click or right-click the name of the package to be published. Select **Publish**.

2.  Review the **Status** column to verify that the package has been published and is now available. If the package is available, the status **published** is displayed.

    If the package is not published successfully, the status **unpublished** is displayed, along with error text that explains why the package is not available.

## To enable only administrators to publish or unpublish packages

1.  Navigate to the following Group Policy Object node:

    **Computer Configuration &gt; Policies &gt; Administrative Templates &gt; System &gt; App-V &gt; Publishing**.

2.  Enable the **Require publish as administrator** Group Policy setting.

    To alternatively use PowerShell to set this item, see [How to Manage App-V 5.1 Packages Running on a Stand-Alone Computer by Using PowerShell](how-to-manage-app-v-51-packages-running-on-a-stand-alone-computer-by-using-powershell.md#bkmk-admins-pub-pkgs).

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)

[How to Configure Access to Packages by Using the Management Console](how-to-configure-access-to-packages-by-using-the-management-console-51.md)
