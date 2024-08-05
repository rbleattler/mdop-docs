---
title: How to uninstall the App-V 5.1 client
description: Use the following procedure to uninstall the Microsoft Application Virtualization (App-V) 5.1 client from a computer.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to uninstall the App-V 5.1 client

Use the following procedure to uninstall the Microsoft Application Virtualization (App-V) 5.1 client from a computer. When you uninstall the App-V 5.1 client all packages published to the computer running the client are also removed. If the uninstall operation does not complete the packages will need to be re-published to the computer running the App-V 5.1 client.

> [!IMPORTANT]
> You should ensure that the App-V 5.1 client service is running prior to performing the uninstall procedure.

## To uninstall the App-V 5.1 client

1.  In Control Panel, double-click **Programs** / **Uninstall a Program**, and then double-click **Microsoft Application Virtualization Client**.

2.  In the dialog box that appears, click **Yes** to continue with the uninstall process.

    > [!IMPORTANT]
    > You can't cancel or interrupt the uninstall process.

3.  A progress bar shows the time remaining. When this step finishes, you must restart the computer so that all associated drivers can be stopped to complete the uninstall process.

    > [!NOTE]
    > You can also use the command line to uninstall the App-V 5.1 client with the following switch: **/UNINSTALL**.

## Related topics

[App-V 5.1 Deployment Checklist](app-v-51-deployment-checklist.md)
