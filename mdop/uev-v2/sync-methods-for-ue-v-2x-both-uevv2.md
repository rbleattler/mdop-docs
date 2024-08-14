---
title: Sync methods for UE-V 2.1 SP1
description: The Microsoft User Experience Virtualization (UE-V) 2.1 SP1 agent lets you synchronize users' application and Windows settings with the settings storage location. The Sync Method configuration defines how the UE-V agent uploads and downloads those settings to the settings storage location.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Sync methods for UE-V 2.1 SP1

The Microsoft User Experience Virtualization (UE-V) 2.1 SP1 agent lets you synchronize users' application and Windows settings with the settings storage location. The *Sync Method* configuration defines how the UE-V agent uploads and downloads those settings to the settings storage location. UE-V 2.1 SP1 has a SyncMethod called the *SyncProvider*. For more information about trigger events that start the synchronization of application and Windows settings, see [Sync trigger events for UE-V 2.1 SP1](sync-trigger-events-for-ue-v-2x-both-uevv2.md).

## SyncMethod configuration

This table explains the changes to SyncMethod from UE-V v1.0 to v2.0 to v2.1, and the settings for each configuration:

| SyncMethod Configuration | V1.0 | V2.0 | V2.1 and V2.1 SP1 | Description |
|--|--|--|--|--|
| SyncProvider | n/a | Default | Default | Settings changes for a specific application or for global Windows desktop settings are saved locally to a cache folder. These changes are then synchronized with the settings storage location when a synchronization trigger event takes place. Pushing out changes saves the local changes to the settings storage path. This default setting is the gold standard for computers. This option attempts to synchronize the setting and times out after a short delay to ensure that the application or operating system startup isn't delayed for a long period of time. This functionality is also tied to the Scheduled task - Sync Controller Application. The administrator controls the frequency of the Scheduled task. By default, computers synchronize their settings every 30 min after logging on. |
| OfflineFiles | Default | Deprecated | Deprecated | Behaves the same as SyncProvider in V2.0. If Offline files are enabled, and the folder is pinned, then UE-V unpins this folder and syncs directly to the central SMB directory. **NOTE:** In V1.0 if you wanted to use UE-V in a CorpNet disconnected manner (also known as traveling with a Laptop), then the guidance is to use Offline Files to ensure that your settings roamed. We received sufficient customer feedback that turning on Offline files is a nontrivial enterprise blocker. So in UE-V 2, we created a tightly coupled synchronization engine to cache your data locally and synchronize the settings to the central server. This feature area doesn't replace Offline Files or Folder Redirection. UE-V 2 doesn't work well with Offline folders so the guidance isn't to set the settings storage path to a pinned Offline or CSC folder. |
| External | n/a | n/a | Supported | New in UE-V 2.1, this configuration method specifies that if UE-V settings are written to a local folder on the user computer, then any external sync engine (such as OneDrive for Business, Work Folders, Sharepoint, or Dropbox) can be used to apply these settings to the different computers that users access. |
| None | Yes | Yes | Yes | This configuration setting is designed for the Virtual Desktop Infrastructure (VDI) and Streamed Application experience primarily. This setting should be used on Windows Server boxes used in a datacenter, where the connection will always be available. Any settings changes are saved directly to the server. If the network connection to the settings storage path isn't available, then the settings changes are cached on the device and are synchronized the next time that the Sync Provider runs. If the settings storage path isn't found and the user profile is removed from a pooled VDI environment on sign out, then these settings changes are lost, and the user must reapply the change when the computer can again reach the settings storage path. Apps and OS wait indefinitely for the location to be present. This could cause App load or OS sign-in time to dramatically increase if the location isn't found. |

You can configure the sync method in these ways:

- When you [deploy the UE-V agent](deploy-required-features-for-ue-v-2x-new-uevv2.md#agent) through a command-line parameter or in a batch script.

- Through [group policy](configuring-ue-v-2x-with-group-policy-objects-both-uevv2.md) settings.

- With the [System Center configuration pack](configuring-ue-v-2x-with-system-center-configuration-manager-2012-both-uevv2.md) for UE-V.

- After installation of the UE-V Agent, by using [Windows PowerShell or Windows Management Instrumentation (WMI)](administering-ue-v-2x-with-windows-powershell-and-wmi-both-uevv2.md).

## Related articles

[Deploy required features for UE-V 2.1 SP1](deploy-required-features-for-ue-v-2x-new-uevv2.md)

[Technical reference for UE-V 2.1 SP1](technical-reference-for-ue-v-2x-both-uevv2.md)
