---
title: Using UE-V 2.1 SP1 with Application Virtualization applications
description: Microsoft User Experience Virtualization (UE-V) 2.1 SP1 supports Microsoft Application Virtualization (App-V) applications without any required modifications to either the App-V package or the UE-V template.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Using UE-V 2.1 SP1 with Application Virtualization applications

Microsoft User Experience Virtualization (UE-V) 2.1 SP1 supports Microsoft Application Virtualization (App-V) applications without any required modifications to either the App-V package or the UE-V template. However, another step is required because you can't run the UE-V generator directly on a virtualized App-V application. Instead, you must install the application locally, generate the template, and then apply the template to the virtualized application. UE-V supports App-V 4.5, App-V 4.6, and App-V 5.0 packages.

## UE-V settings synchronization for App-V applications

UE-V monitors when an application opens by the program name and, optionally, by file version numbers and product version numbers, whether the application is installed locally or virtually by using App-V. When the application starts, UE-V monitors the App-V process, applies any settings that are stored in the user's settings storage path, and then enables the application to start normally. UE-V monitors App-V applications and automatically translates the relevant file and registry paths to the virtualized location as opposed to the physical location outside the App-V computing environment.

### To implement settings synchronization for a virtualized application

1.  Run the UE-V generator to collect the settings of the locally installed application whose settings you want to synchronize between computers. This process creates a settings location template. If you use a built-in template such as the Microsoft Office 2010 template, skip this step. For more information about running the UE-V generator, see [Deploy UE-V 2.1 SP1 for custom applications](deploy-ue-v-2x-for-custom-applications-new-uevv2.md#createcustomtemplates).

2.  Install the App-V application package if you haven't already done so.

3.  Publish the template to the location of your settings template catalog or manually install the template by using the `Register-UEVTemplate` Windows PowerShell cmdlet.

    > [!NOTE]
    > If you publish the newly created template to the settings template catalog, the client does not receive the template until the sync provider updates the settings. To manually start this process, open **Task Scheduler**, expand **Task Scheduler Library**, expand **Microsoft**, and expand **UE-V**. In the results pane, right-click **Template Auto Update**, and then click **Run**.

4.  Start the App-V package.

## Related articles

[Administering UE-V 2.1 SP1](administering-ue-v-2x-new-uevv2.md)
