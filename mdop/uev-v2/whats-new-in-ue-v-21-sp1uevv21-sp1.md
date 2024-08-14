---
title: What's new in UE-V 2.1 SP1
description: User Experience Virtualization 2.1 SP1 provides these new features and functionality compared to UE-V 2.1.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# What's new in UE-V 2.1 SP1

Microsoft User Experience Virtualization (UE-V) 2.1 SP1 provides these new features and functionality compared to UE-V 2.1. For more information about the UE-V 2.1 SP1 release, see the [UE-V 2.1 SP1 release notes](microsoft-user-experience-virtualization--ue-v--21-sp1-release-notes.md) provide.

## Support for Windows 10

UE-V 2.1 SP1 adds support for Windows 10, in addition to the same software that is supported in earlier versions of UE-V.

### Compatibility with Microsoft Azure

Windows 10 lets enterprise users synchronize Windows app settings and Windows operating system settings to Azure instead of to OneDrive. You can use the Windows 10 enterprise sync functionality together with UE-V for on-premises domain-joined computers only. To enable coexistence between Windows 10 and UE-V, you must disable the following UE-V templates using either PowerShell on each client or group policy.

In group policy, under the Microsoft User Experience Virtualization node, configure these policy settings:

- Enable "Do Not Synchronize Windows Apps"

- Disable "Sync Windows Settings"

### Settings synchronization behavior changed for Windows 10 support

UE-V 2.1 SP1 roams taskbar settings between Windows 10 devices. However, UE-V doesn't synchronize taskbar settings between Windows 10 devices and devices running previous operating systems.

In addition, UE-V 2.1 SP1 doesn't synchronize settings between the Microsoft Calculator in Windows 10 and the Microsoft Calculator in previous operating systems.

## Support added for roaming network printers

UE-V 2.1 SP1 lets network printers roam between devices so that a user has access to their network printers when logged on to any device on the network. This includes roaming the printer that they set as the default.

Printer roaming in UE-V requires one of these scenarios:

- The print server can download the required driver when it roams to a new device.

- The driver for the roaming network printer is preinstalled on any device that needs to access that network printer.

- The printer driver can be obtained from Windows Update.

> [!NOTE]
> The UE-V printer roaming feature doesn't roam printer settings or preferences, such as printing double-sided.

## Office 2013 settings location template

UE-V 2.1 and 2.1 SP1 include the Microsoft Office 2013 settings location template with improved Outlook signature support. UE-V can synchronize default signature settings for new, reply, and forwarded emails. Users don't have to choose the default signature settings.

> [!NOTE]
> An Outlook profile must be created for any device on which a user wants to sync their Outlook signature. If the profile isn't already created, the user can create one and then restart Outlook on that device to enable signature synchronization.

Previously UE-V included Microsoft Office 2010 settings location templates that were automatically distributed and registered with the UE-V Agent. UE-V 2.1 works with Office 365 to determine whether Office 365 roams settings for Office 2013 settings. If Office 365 roams settings, then UE-V doesn't roam them. [Overview of user and roaming settings for Office 2013](/previous-versions/office/office-2013-resource-kit/jj733593(v=office.15)) provides more information.

To enable settings synchronization using UE-V 2.1, do one of the following actions:

- Use group policy to disable Office 365 synchronization

- Don't enable the Office 365 synchronization experience during Office 2013 installation

UE-V 2.1 ships [Office 2013 and Office 2010 templates](prepare-a-ue-v-2x-deployment-new-uevv2.md#autosyncsettings). This release removes the Office 2007 templates. To get the templates, download the [User Experience Virtualization (UE-V) settings templates for Microsoft Office](https://www.microsoft.com/download/details.aspx?id=46367).

## Related articles

[Get started with UE-V 2.1 SP1](get-started-with-ue-v-2x-new-uevv2.md)

[Prepare a UE-V 2.1 SP1 deployment](prepare-a-ue-v-2x-deployment-new-uevv2.md)

[UE-V 2.1 SP1 release notes](microsoft-user-experience-virtualization--ue-v--21-sp1-release-notes.md)
