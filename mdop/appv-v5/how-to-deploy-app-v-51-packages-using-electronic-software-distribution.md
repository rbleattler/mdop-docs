---
title: How to deploy App-V 5.1 packages using electronic software distribution
description: You can use an electronic software distribution (ESD) system to deploy App-V 5.1 virtual applications to App-V clients.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# How to deploy App-V 5.1 packages using electronic software distribution

You can use an electronic software distribution (ESD) system to deploy App-V 5.1 virtual applications to App-V clients. For details, see the documentation available with the ESD you are using.

For component requirements and options for using an ESD to deploy App-V packages, see [Planning to Deploy App-V 5.1 with an Electronic Software Distribution System](planning-to-deploy-app-v-51-with-an-electronic-software-distribution-system.md).

Use one of the following methods to publish packages to App-V client computers with an ESD:

| Method | Description |
|--|--|
| Functionality provided by a third-party ESD | Use the functionality in a third-party ESD. |
| Stand-alone Windows Installer | Install the application on the target client computer by using the associated Windows Installer (.msi) file that is created when you initially sequence an application. The Windows Installer file contains the associated App-V 5.1 package file information used to configure a package and copies the required package files to the client. |
| PowerShell | Use PowerShell cmdlets to deploy virtualized applications. For more information about using PowerShell and App-V 5.1, see [Administering App-V 5.1 by Using PowerShell](administering-app-v-51-by-using-powershell.md). |

> [!NOTE]
> If you use System Center Configuration Manager, start by reviewing [Introduction to Application Management in Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg682125(v=technet.10)) for information about using App-V 5.1 and System Center 2012 Configuration Manager.

## To deploy App-V 5.1 packages by using an ESD

1.  Install the App-V 5.1 Sequencer on a computer in your environment. For more information about installing the sequencer, see [How to Install the Sequencer](how-to-install-the-sequencer-51beta-gb18030.md).

2.  Use the App-V 5.1 Sequencer to create virtual application. For information about creating a virtual application, see [Creating and Managing App-V 5.1 Virtualized Applications](creating-and-managing-app-v-51-virtualized-applications.md).

3.  After you create the virtual application, deploy the package by using your ESD solution.

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)
