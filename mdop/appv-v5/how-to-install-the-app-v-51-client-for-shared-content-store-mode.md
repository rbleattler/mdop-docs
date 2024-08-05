---
title: How to install the App-V 5.1 client for shared content store mode
description: Use the following procedure to install the Microsoft Application Virtualization (App-V) 5.1 client so that it uses the App-V 5.1 Shared Content Store (SCS) mode.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# How to install the App-V 5.1 client for shared content store mode

Use the following procedure to install the Microsoft Application Virtualization (App-V) 5.1 client so that it uses the App-V 5.1 Shared Content Store (SCS) mode. You should ensure that all required prerequisites are installed on the computer you plan to install to. Use the following link to see [App-V 5.1 Prerequisites](app-v-51-prerequisites.md).

> [!NOTE]
> Before performing this procedure if necessary uninstall any existing version of the App-V 5.1 client.

## Install and configure the App-V 5.1 client for SCS mode

1.  Copy the App-V 5.1 client installation files to the computer on which it will be installed. Open a command line and from the directory where the installation files are saved type one of the following options depending on the version of the client you are installing:

    -   To install the RDS version of the App-V 5.1 client type: **appv\_client\_setup\_rds.exe /SHAREDCONTENTSTOREMODE=1 /q**

    -   To install the standard version of the App-V 5.1 client type: **appv\_client\_setup.exe /SHAREDCONTENTSTOREMODE=1 /q**

        > [!NOTE]
        > You must perform a silent installation or the installation will fail.

2.  After you have completed the installation you can deploy packages to the computer running the client and all package contents will be streamed across the network.

## Related topics

[Deploying the App-V 5.1 Sequencer and Client](deploying-the-app-v-51-sequencer-and-client.md)
