---
title: App-V 4.6 SP2 Release Notes
description: App-V 4.6 SP2 Release Notes
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.date: 08/30/2016
---


# App-V 4.6 SP2 Release Notes


Read these release notes thoroughly before you install Microsoft Application Virtualization (App-V) 4.6 SP2.

These release notes contain information that is required to successfully install Application Virtualization 4.6 SP2. The release notes also contain information that isn't available in the product documentation. If there's a difference between these release notes and other App-V 4.6 SP2 documentation, the latest change should be considered authoritative. These release notes supersede the content that is included with this product.


## <a name="known-issues-with-app-v-4-6-sp2-"></a>Known Issues with App-V 4.6 SP2


### Short file name support is disabled for nonsystem physical drives when you sequence

When you sequence on Windows 8 or Windows Server 2012, support for short file names (8.3) is disabled by default for nonsystem physical drives.

The underlying physical drive associated with the primary virtual application directory (for example, "Q:\\appname") on the sequencing station must provide short file name (8.3) support in order for the App-V 4.6 SP2 Sequencer to generate short file names when creating virtual application packages. Short file name (8.3) support is disabled by default for nonsystem physical drives on Windows 8 or Windows Server 2012.

**Workaround:** Enable short file name (8.3) support on nonsystem physical drives. You can use the following command to enable short file name support on Windows 8 or Windows Server 2012.

```cmd
fsutil 8dot3name set <virtual drive letter>:
```

For example, use the following command if the drive letter is "Q:":

```cmd
fsutil 8dot3name set Q: 0
```

> [!NOTE]
> You don't need to change this setting on the App-V client because the App-V file system properly handles short paths on Windows 8 or Windows Server 2012.

### App-V doesn't override the default handler for file type or protocol associations on Windows 8

If you select a default application by using **Default Programs** in **Control Panel** on Windows 8, App-V won't override the associated file type associations for that application.

**Workaround:** None.

### Virtualized Outlook 2010 isn't offered as an option for mailto clickable links on Windows 8

The mailto shell extension doesn't offer virtualized Outlook 2010 on Windows 8. For example, if you select a mailto: link from virtualized Outlook 2010 that is running on Windows 8, a new email window isn't created. This option works correctly on Windows 7 and earlier versions of the Windows operating system.

**Workaround:** None.

### Application Virtualization 4.6 SP2 update isn't offered on all locales that use Microsoft Update

When you use Microsoft Update, the update for App-V 4.6 SP2 isn't available for the following language locales:

-   Kazakh

-   Hindi

-   Serbian-Cyrillic

**Workaround:** If you're using Microsoft Windows Server Update Services (WSUS), use the English version of the update or download the update from the Microsoft Update Catalog.

## Related information

[About Microsoft Application Virtualization 4.6 SP2](about-microsoft-application-virtualization-46-sp2.md)
