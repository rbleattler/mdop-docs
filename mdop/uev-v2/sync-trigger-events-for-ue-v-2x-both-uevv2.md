---
title: Sync trigger events for UE-V 2.1 SP1
description: Microsoft User Experience Virtualization (UE-V) 2.1 SP1 lets you synchronize your application and Windows settings across all your domain-joined devices. Sync trigger events define when the UE-V agent synchronizes those settings with the settings storage location.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Sync trigger events for UE-V 2.1 SP1

Microsoft User Experience Virtualization (UE-V) 2.1 SP1 lets you synchronize your application and Windows settings across all your domain-joined devices. *Sync trigger events* define when the UE-V agent synchronizes those settings with the settings storage location. UE-V 2 introduces a new *Sync Method* called the *SyncProvider*. For more information about sync method configuration, see [Sync methods for UE-V 2.1 SP1](sync-methods-for-ue-v-2x-both-uevv2.md).

## UE-V 2 sync trigger events

The following table explains the trigger events for classic applications and Windows settings.

| **UE-V 2 Trigger Event** | **SyncMethod=SyncProvider** | **SyncMethod=None** |
|--|--|--|
| **Windows Logon** | - Application and Windows settings are imported to the local cache from the settings storage location. <br> - [Asynchronous Windows settings](prepare-a-ue-v-2x-deployment-new-uevv2.md#autosyncsettings2) are applied. <br> - Synchronous Windows settings are applied during the next Windows sign in. <br> - Application settings are applied when the application starts. | - Application and Windows settings are read directly from the settings storage location. <br> - Asynchronous and synchronous Windows settings are applied. <br> - Application settings are applied when the application starts. |
| **Windows Logoff** | Store changes locally and cache and copy asynchronous and synchronous Windows settings to the settings storage location server, if available | Store changes to asynchronous and synchronous Windows settings storage location |
| **Windows Connect (RDP) / Unlock** | Synchronize any asynchronous Windows settings from settings storage location to local cache, if available. <br> Apply cached Windows settings | Download and apply asynchronous windows settings from settings storage location |
| **Windows Disconnect (RDP) / Lock** | Store asynchronous Windows settings changes to the local cache. <br> Synchronize any asynchronous Windows settings from the local cache to settings storage location, if available | Store asynchronous Windows settings changes to the settings storage location |
| **Application start** | Apply application settings from local cache as the application starts | Apply application settings from settings storage location as the application starts |
| **Application closes** | Store any application settings changes to the local cache and copy settings to settings storage location, if available | Store any application settings changes to settings storage location |
| **Sync Controller Scheduled Task or "Sync Now" is run from the Company Settings Center** | Application and Windows settings are synchronized between the settings storage location and the local cache. <br> **Note:** Settings changes aren't cached locally until an application closes. This trigger doesn't export changes made to a currently running application. <br> For Windows settings, this means that any changes aren't cached locally and exported until the next lock (Asynchronous) or sign out (Asynchronous and Synchronous). <br> Settings are applied in these cases: <br> - Asynchronous Windows settings are applied directly. <br> - Application settings are applied when the application starts. <br> - Both asynchronous and synchronous Windows settings are applied during the next Windows sign in. <br> - Windows app (AppX) settings are applied during the next refresh. For more information, see [Monitor application settings](changing-the-frequency-of-ue-v-2x-scheduled-tasks-both-uevv2.md). | NA |
| **Asynchronous Settings updated on remote store** | Load and apply new asynchronous settings from the cache. | Load and apply settings from central server |

## Related articles

[Technical reference for UE-V 2.1 SP1](technical-reference-for-ue-v-2x-both-uevv2.md)

[Changing the frequency of UE-V 2.1 SP1 scheduled tasks](changing-the-frequency-of-ue-v-2x-scheduled-tasks-both-uevv2.md)

[Choose the configuration method for UE-V 2.1 SP1](deploy-required-features-for-ue-v-2x-new-uevv2.md#config)
