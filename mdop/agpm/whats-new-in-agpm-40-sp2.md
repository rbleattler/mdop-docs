---
title: What's New in AGPM 4.0 SP2
description: What's New in AGPM 4.0 SP2
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---


# What's New in AGPM 4.0 SP2


This content describes enhancements and supported configurations for Microsoft Advanced Group Policy Management (AGPM) 4.0 Service Pack 2 (SP2). If there's a difference between this content and other AGPM documentation, consider this content authoritative and assume that it supersedes the other documentation.

## What's new


AGPM 4.0 SP2 supports the following features and functionality.

### Support for Windows 8.1 and Windows Server 2012 R2

AGPM 4.0 SP2 adds support for the Windows 8.1 and Windows Server 2012 R2 operating systems.

### New and changed client-side extensions

Group Policy client-side extensions have been added or changed for AGPM to support new policy settings in Windows 8.1. These policy settings enable Group Policy administrators to manage and track Windows 8.1-specific policy settings that change between two Group Policy Objects (GPOs) or templates. To view your client-side extensions, use the settings and difference reports that are available in the AGPM Client.

The new and changed Group Policy client-side extensions are:

-   **Specify Work Folders settings**. If you enable this policy setting, IT administrators can configure Work Folders to be created automatically. The Work Folders feature enables end users to synchronize files from their Windows desktop devices to their other devices. Use this policy setting to create the synchronization relationship on an end user's devices and to configure how to identify the file server that stores the user's Work Folders. If you select the **Auto provision synchronization** check box, the synchronization partnership is created without user input, and data will automatically start synchronizing to the user's device. If you don't select the **Auto provision synchronization** check box, users must provide input to start the synchronization.

-   **Force automatic setup for all users**. If you enable this policy setting, IT administrators can determine whether to create the Work Folders partnership automatically on end-user devices without input from end users. If you enable this policy setting, the synchronization is set up according to how you configure the **Specify Work Folders settings** policy setting. If you set the **Force automatic setup for all users** policy setting to **Disabled** or **Not configured**, the Work Folders partnership is configured according to how you set the **Automatic Provisioning** option in the **Specify Work Folders settings** policy setting.

For more information about the Work Folders feature, see [Work Folders Overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265974(v=ws.11)).

### Customer feedback and hotfix rollup

AGPM 4.0 SP2 includes a rollup of hotfixes to address issues found since the AGPM 4.0 Service Pack 1 (SP1) release. AGPM 4.0 SP2 contains the latest fixes up to and including Microsoft Advanced Group Policy Management 4.0 SP1 Hotfix 1.

### New Group Policy extensions in settings and difference reports

The new Group Policy extensions have been added to the settings and difference reports.

### Installer changes and support

The changes and support for the AGPM 4.0 SP2 installer are:

-   If you install AGPM 4.0 SP2 on the Windows 8 or Windows Server 2012 operating system or later operating systems, the AGPM installer verifies that the required prerequisite software (the Group Policy Management Console (GPMC) and the Microsoft .NET Framework 3.5) is installed. If this prerequisite software isn't installed, the AGPM 4.0 SP2 installation is blocked.

-   When you install the AGPM Server, WCF Activation, Non-HTTP Activation, and Windows Process Activation Service are automatically enabled.

-   On the Windows Vista client operating system and later operating systems, download the appropriate version of the Remote System Administration Tools for your operating system before you install AGPM 4.0 SP2.

-   AGPM 4.0 SP2 supports backward compatibility with older supported operating systems.

### Ability to upgrade to AGPM 4.0 SP2 without reentering configuration parameters

You can upgrade the AGPM Client or AGPM Server to AGPM 4.0 SP2 without being prompted to reenter configuration parameters (called the Smart Upgrade) only from AGPM 4.0 onward, as shown in the following table. If you're upgrading to AGPM 4.0 SP2 from other versions of AGPM, as shown in the table, you must use the Classic Upgrade, which requires you to reenter the configuration parameters. Because each version of AGPM is associated with a particular operating system, see [Choosing Which Version of AGPM to Install](choosing-which-version-of-agpm-to-install.md) and make sure that you upgrade your operating system as appropriate before you upgrade AGPM.

#### AGPM 4.0 SP2 supported upgrades

| **AGPM version from which you can upgrade** | **2.5** | **3.0** | **4.0** | **4.0 SP1** | **4.0 SP2** |
|--|--|--|--|--|--|
| 2.5 | Not applicable | Classic Upgrade | Classic Upgrade | Installation is blocked | Installation is blocked |
| 3.0 | Not applicable | Not applicable | Classic Upgrade | Installation is blocked | Installation is blocked |
| 4.0 | Not applicable | Not applicable | Not applicable | Smart Upgrade | Smart Upgrade |
| 4.0 SP1 | Not applicable | Not applicable | Not applicable | Not applicable | Smart Upgrade |

## Supported configurations


AGPM 4.0 SP2 supports the configurations in the following table. Although AGPM supports mixed configurations, we strongly recommend that you run the AGPM Client and AGPM Server on the same operating system line—for example, Windows 8.1 with Windows Server 2012 R2, Windows 8 with Windows Server 2012, and so on.

### AGPM 4.0 SP2 supported operating systems and policy settings

| **Supported configurations for the AGPM Server** | **Supported configurations for the AGPM Client** | **AGPM Support** |
|--|--|--|
| Windows Server 2012 R2 or Windows 8.1 | Windows Server 2012 R2 or Windows 8.1 | Supported |
| Windows Server 2012 R2, Windows Server 2012, Windows 8.1, or Windows 8 | Windows Server 2012 or Windows 8 | Supported, but cannot edit policy settings or preference items that exist only in Windows 8.1 |
| Windows Server 2008 R2 or Windows 7 | Windows Server 2008 R2 or Windows 7 | Supported, but cannot edit policy settings or preference items that exist only in Windows 8.1 or Windows 8 |
| Windows Server 2012, Windows Server 2008 R2, Windows 8, or Windows 7 | Windows Server 2008 or Windows Vista with Service Pack 1 (SP1) | Supported, but cannot edit policy settings or preference items that exist only in Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 8.1, Windows 8, or Windows 7 |
| Windows Server 2008 or Windows Vista with Service Pack 1 (SP1) | Windows Server 2012, Windows Server 2008 R2, Windows 8, or Windows 7 | Not supported |
| Windows Server 2008 or Windows Vista with Service Pack 1 (SP1) | Windows Server 2008 or Windows Vista with Service Pack 1 (SP1) | Supported, but cannot report or edit policy settings or preference items that exist only in Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 8.1, Windows 8, or Windows 7 |

## Prerequisites for installing AGPM 4.0 SP2

- If the .NET Framework 3.5 isn't enabled or installed, the installer blocks the installation.

- If the GPMC isn't enabled or installed, the installer blocks the installation.

## How to get MDOP

AGPM 4.0 SP2 is a part of the Microsoft Desktop Optimization Pack (MDOP). MDOP is part of Microsoft Software Assurance. For more information about Microsoft Software Assurance and acquiring MDOP, see [How to get MDOP](../index.md#how-to-get-mdop).

## Related information

[Advanced Group Policy Management](index.md)

[Release Notes for Microsoft Advanced Group Policy Management 4.0 SP2](release-notes-for-microsoft-advanced-group-policy-management-40-sp2.md)

[Choosing Which Version of AGPM to Install](choosing-which-version-of-agpm-to-install.md)
