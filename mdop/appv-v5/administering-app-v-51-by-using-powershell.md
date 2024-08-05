---
title: Administering App-V 5.1 by using Windows PowerShell
description: Microsoft Application Virtualization (App-V) 5.1 provides Windows PowerShell cmdlets, which can help administrators perform various App-V 5.1 tasks.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Administering App-V 5.1 by using Windows PowerShell

Microsoft Application Virtualization (App-V) 5.1 provides Windows PowerShell cmdlets, which can help administrators perform various App-V 5.1 tasks. The following sections provide more information about using PowerShell with App-V 5.1.

## How to administer App-V 5.1 by using PowerShell

Use the following PowerShell procedures to perform various App-V 5.1 tasks.

| Name | Description |
|------|-------------|
| [How to Load the PowerShell Cmdlets and Get Cmdlet Help](how-to-load-the-powershell-cmdlets-and-get-cmdlet-help-51.md) | Describes how to install the PowerShell cmdlets and find cmdlet help and examples. |
| [How to Manage App-V 5.1 Packages Running on a Stand-Alone Computer by Using PowerShell](how-to-manage-app-v-51-packages-running-on-a-stand-alone-computer-by-using-powershell.md) | Describes how to manage the client package lifecycle on a stand-alone computer using PowerShell. |
| [How to Manage Connection Groups on a Stand-alone Computer by Using PowerShell](how-to-manage-connection-groups-on-a-stand-alone-computer-by-using-powershell51.md) | Describes how to manage connection groups using PowerShell. |
| [How to Modify Client Configuration by Using PowerShell](how-to-modify-client-configuration-by-using-powershell51.md) | Describes how to modify the client using PowerShell. |
| [How to Apply the User Configuration File by Using PowerShell](how-to-apply-the-user-configuration-file-by-using-powershell51.md) | Describes how to apply a user configuration file using PowerShell. |
| [How to Apply the Deployment Configuration File by Using PowerShell](how-to-apply-the-deployment-configuration-file-by-using-powershell51.md) | Describes how to apply a deployment configuration file using PowerShell. |
| [How to Sequence a Package by Using PowerShell](how-to-sequence-a-package--by-using-powershell-51.md) | Describes how to create a new package using PowerShell. |
| [How to Create a Package Accelerator by Using PowerShell](how-to-create-a-package-accelerator-by-using-powershell51.md) | Describes how to create a package accelerator using PowerShell. You can use package accelerators automatically sequence large, complex applications. |
| [How to Enable Reporting on the App-V 5.1 Client by Using PowerShell](how-to-enable-reporting-on-the-app-v-51-client-by-using-powershell.md) | Describes how to enable the computer running the App-V 5.1 to send reporting information. |
| [How to Install the App-V Databases and Convert the Associated Security Identifiers by Using PowerShell](how-to-install-the-app-v-databases-and-convert-the-associated-security-identifiers--by-using-powershell51.md) | Describes how to take an array of account names and to convert each of them to the corresponding SID in standard and hexadecimal formats. |

> [!IMPORTANT]
> Make sure that any script you execute with your App-V packages matches the execution policy that you have configured for PowerShell.

## PowerShell error handling

Use the following table for information about App-V 5.1 PowerShell error handling.

| Event | Action |
|--|--|
| Using the RollbackOnError attribute with embedded scripts | When you use the **RollbackOnError** attribute with embedded scripts, the attribute is ignored for the following events: <ul><li>Removing a package</li><li>Unpublishing a package</li><li>Terminating a virtual environment</li><li>Terminating a process</li></ul> |
| Package name contains **$** | If a package name contains the character (`$`), you must use a single-quote ( `'` ), for example, <br> `Add-AppvClientPackage 'Contoso$App.appv'` |

## Related articles

[Operations for App-V 5.1](operations-for-app-v-51.md)
