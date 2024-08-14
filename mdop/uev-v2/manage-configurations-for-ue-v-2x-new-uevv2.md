---
title: Manage configurations for UE-V 2.1 SP1
description: With Microsoft User Experience Virtualization (UE-V) 2.1 SP1, you have to manage the configuration of the UE-V agent and also manage storage locations for resources such as settings package files.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Manage configurations for UE-V 2.1 SP1

With Microsoft User Experience Virtualization (UE-V) 2.1 SP1, you have to manage the configuration of the UE-V agent and also manage storage locations for resources such as settings package files. You might have to perform other tasks, for example, configuring the Company Settings Center to define how users interact with UE-V. The following articles provide guidance for managing these UE-V resources.

## Configuring UE-V 2.1 SP1 by using group policy objects

You can use group policy objects to modify the settings that define how UE-V synchronizes settings on computers.

[Configuring UE-V 2.1 SP1 with group policy objects](configuring-ue-v-2x-with-group-policy-objects-both-uevv2.md)

## Configuring UE-V 2.1 SP1 with System Center Configuration Manager 2012

You can use System Center 2012 Configuration Manager to manage the UE-V agent by using the UE-V 2 Configuration Pack.

[Configuring UE-V 2.1 SP1 with System Center Configuration Manager 2012](configuring-ue-v-2x-with-system-center-configuration-manager-2012-both-uevv2.md)

## Administering UE-V 2.1 SP1 with PowerShell and WMI

UE-V provides Windows PowerShell cmdlets, which can help administrators perform various UE-V tasks.

[Administering UE-V 2.1 SP1 with Windows PowerShell and WMI](administering-ue-v-2x-with-windows-powershell-and-wmi-both-uevv2.md)

## Configuring the Company Settings Center for UE-V 2.1 SP1

You can configure the Company Settings Center that is installed by using the UE-V agent to define how users interact with UE-V.

[Configuring the Company Settings Center for UE-V 2.1 SP1](configuring-the-company-settings-center-for-ue-v-2x-both-uevv2.md)

## Examples of configuration settings for UE-V 2.1 SP1

Here are some examples of UE-V configuration settings:

- **Settings Storage Path:** Specifies the location of the file share that stores the UE-V settings.

- **Settings Template Catalog Path:** Specifies the Universal Naming Convention (UNC) path that defines the location that was checked for new settings location templates.

- **Register Microsoft Templates:** Specifies whether the default Microsoft templates should be registered during installation.

- **Synchronization Method:** Specifies whether UE-V uses the sync provider or none. The "SyncProvider" supports computers that are disconnected from the network. "None" applies when the computer is always connected to the network. For more information about the Sync Method, see [Sync methods for UE-V 2.1 SP1](sync-methods-for-ue-v-2x-both-uevv2.md).

- **Synchronization Timeout:** Specifies the number of milliseconds that the computer waits before time-out when it retrieves the user settings from the settings storage location.

- **Synchronization Enable:** Specifies whether the UE-V settings synchronization is enabled or disabled.

- **Maximum Package Size:** Specifies a settings package file threshold size in bytes at which the UE-V agent reports a warning.

- **Don't Sync Windows App Settings:** Specifies that UE-V shouldn't synchronize Windows apps.

- **Enable/Disable First Use Notification:** Specifies whether UE-V displays a dialog box the first time that the UE-V agent runs on a user's computer.

- **Enable/Disable Tray Icon:** Specifies whether UE-V displays an icon in the notification area and any notifications associated with it. The icon provides a link to the Company Settings Center.

- **Custom Contact IT Hyperlink:** Defines the path, text, and description for the **Contact IT** hyperlink in the Company Settings Center.

## Related articles

[Administering UE-V 2.1 SP1](administering-ue-v-2x-new-uevv2.md)

[Deploy required features for UE-V 2.1 SP1](deploy-required-features-for-ue-v-2x-new-uevv2.md)

[Deploy UE-V 2.1 SP1 for custom applications](deploy-ue-v-2x-for-custom-applications-new-uevv2.md)
