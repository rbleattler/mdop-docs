---
title: What's new in AGPM 4.0 SP3
description: This content describes enhancements and supported configurations for Microsoft Advanced Group Policy Management (AGPM) 4.0 Service Pack 3 (SP3).
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 09/27/2016
---

# What's New in AGPM 4.0 SP3

This content describes enhancements and supported configurations for Microsoft Advanced Group Policy Management (AGPM) 4.0 Service Pack 3 (SP3). If there's a difference between this content and other AGPM documentation, consider this content authoritative and assume that it supersedes the other documentation.

## <a href="" id="what-s-new"></a>What's new

AGPM 4.0 SP3 supports the following features and functionality.

### Support for Windows Server 2022

AGPM 4.0 SP3 adds support for Windows Server 2022

### Support for Windows 11

AGPM 4.0 SP3 adds support for the Windows 11.

### Support for Windows 10

AGPM 4.0 SP3 adds support for the Windows 10 and Windows Server 2016 operating systems.

### Support for PowerShell

AGPM 4.0 SP3 adds support for PowerShell cmdlets. For a list of the cmdlets available in AGPM 4.0 SP3, including descriptions and syntax, see [Microsoft Desktop Optimization Pack Automation with Windows PowerShell](/powershell/mdop/get-started).

### Customer feedback and hotfix rollup

AGPM 4.0 SP3 includes a rollup of all fixes up to and including Microsoft Advanced Group Policy Management 4.0 SP2 and any fixes for issues found since AGPM 4.0 SP2.

### Ability to upgrade to AGPM 4.0 SP3 without reentering configuration parameters

You can upgrade the AGPM client or AGPM server to AGPM 4.0 SP3 without being prompted to reenter configuration parameters only from AGPM 4.0 and later, as shown in the following table. This process is also called the "Smart Upgrade." If you're upgrading to AGPM 4.0 SP3 from other versions of AGPM, as shown in the table, you must use the classic upgrade, which requires you to reenter the configuration parameters. Because each version of AGPM is associated with a particular operating system, see [Choosing which version of AGPM to install](choosing-which-version-of-agpm-to-install.md). Make sure that you upgrade your operating system as appropriate before you upgrade AGPM.

#### AGPM 4.0 SP3 supported upgrades

| AGPM version from which you can upgrade | 2.5 | 3.0 | 4.0 | 4.0 SP1 | 4.0 SP2 | 4.0 SP3 |
|--|--|--|--|--|--|--|
| 2.5 | Not applicable |  Classic upgrade |  Classic upgrade | Installation is blocked | Installation is blocked | Installation is blocked |
| 3.0 | Not applicable | Not applicable |  Classic upgrade | Installation is blocked | Installation is blocked | Installation is blocked |
| 4.0 | Not applicable | Not applicable | Not applicable | Smart Upgrade | Smart Upgrade | Smart Upgrade |
| 4.0 SP1 | Not applicable | Not applicable | Not applicable | Not applicable | Smart Upgrade | Smart Upgrade |
| 4.0 SP2 | Not applicable | Not applicable | Not applicable | Not applicable | Not applicable | Smart Upgrade |

## Supported configurations

AGPM 4.0 SP3 supports the configurations in the following table. Although AGPM supports mixed configurations, we strongly recommend that you run the AGPM client and AGPM server on the same operating system line. For example, Windows 10 with Windows Server 2016 or Windows 8.1 with Windows Server 2012 R2.

### AGPM 4.0 SP3 supported operating systems and policy settings

| Supported configurations for the AGPM server | Supported configurations for the AGPM client | AGPM Support |
|--|--|--|
| Windows Server 2019, Windows Server 2022, Windows 10, Windows 11 | Windows 10, Windows 11 | Supported |
| Windows Server 2016 or Windows 10 | Windows 10 | Supported |
| Windows Server 2012 R2 or Windows 8.1 | Windows Server 2012 R2 or Windows 8.1 | Supported |
| Windows Server 2012 R2, Windows Server 2012, or Windows 8.1 | Windows Server 2012 | Supported, but can't edit policy settings or preference items that exist only in Windows 8.1 |
| Windows Server 2008 R2 or Windows 7 | Windows Server 2008 R2 or Windows 7 | Supported, but can't edit policy settings or preference items that exist only in Windows 8.1 |
| Windows Server 2012, Windows Server 2008 R2, or Windows 7 | Windows Server 2008 or Windows Vista with Service Pack 1 (SP1) | Supported, but can't edit policy settings or preference items that exist only in Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 8.1, or Windows 7 |
| Windows Server 2008 or Windows Vista with SP1 | Windows Server 2012, Windows Server 2008 R2, or Windows 7 | Not supported |
| Windows Server 2008 or Windows Vista with SP1 | Windows Server 2008 or Windows Vista with SP1 | Supported, but can't report or edit policy settings or preference items that exist only in Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 8.1, or Windows 7 |

## Prerequisites for installing AGPM 4.0 SP3

The following table describes the behavior of AGPM 4.0 SP3 Client and Server installers when the .NET Framework 4.5.1, PowerShell 3.0, or the GPMC in the Remote Server Administration Tools is missing.

### AGPM client

| Operating system | .NET Framework | PowerShell |
|--|--|--|
| Windows 10 | If the .NET Framework 4.5.1 isn't enabled or installed, the installer blocks the installation. | If PowerShell 3.0 isn't installed, the installer blocks the installation. |
| Windows 8.1 | If the .NET Framework 4.5.1 isn't enabled or installed, the installer blocks the installation. | If PowerShell 3.0 isn't installed, the installer blocks the installation. |
| Windows Server 2012 R2 | If the .NET Framework 4.5.1 isn't enabled or installed, the installer blocks the installation. | If PowerShell 3.0 isn't installed, the installer blocks the installation. |

### AGPM server

| Operating system | Remote Server Administration Tools | .NET Framework | Remote Server Administration Tools |
|--|--|--|--|
| Windows 10 | If the GPMC isn't enabled or installed, the installer blocks the installation. | If the .NET Framework 4.5.1 isn't enabled or installed, the installer blocks the installation. | If the GPMC isn't enabled or installed, the installer blocks the installation. |
| Windows 8.1 | If the GPMC isn't enabled or installed, the installer blocks the installation. | If the .NET Framework 4.5.1 isn't enabled or installed, the installer blocks the installation. | If the GPMC isn't enabled or installed, the installer blocks the installation. |
| Windows Server 2012 R2 | If the GPMC isn't enabled, the installer enables it during the installation. | If the .NET Framework 4.5.1 isn't enabled or installed, the installer blocks the installation. | If the GPMC isn't enabled, the installer enables it during the installation. |

## Related articles

[Release notes for Microsoft Advanced Group Policy Management 4.0 SP3](release-notes-for-microsoft-advanced-group-policy-management-40-sp3.md)

[Choosing which version of AGPM to install](choosing-which-version-of-agpm-to-install.md)
