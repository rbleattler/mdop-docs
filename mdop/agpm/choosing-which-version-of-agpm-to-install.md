---
title: Choosing which version of AGPM to install
description: Each release of Microsoft Advanced Group Policy Management (AGPM) supports specific versions of the Windows operating system
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/05/2017
---

# Choosing which version of AGPM to install

[!INCLUDE [mdop-lifecycle-statement](../includes/mdop-lifecycle-statement.md)]

Each release of Microsoft Advanced Group Policy Management (AGPM) supports specific versions of the Windows operating system. We strongly recommend that you run the AGPM Client and AGPM Server on the same line of operating systems. For example, Windows 10 with Windows Server 2016, Windows 8.1 with Windows Server 2012 R2, and so on.

We recommend that you install the AGPM Server on the most recent version of the operating system in the domain that AGPM is supported on. AGPM uses the Group Policy Management Console (GPMC) to back up and restore group policy objects (GPOs). Because newer versions of the GPMC provide additional policy settings that aren't available in earlier versions, you can manage more policy settings by using the most recent version of the operating system.

All versions of AGPM can manage only the policy settings that were introduced in the same version or an earlier version of the operating system on which AGPM is running. For example, if you install AGPM 4.0 SP2 on Windows Server 2012, you can manage policy settings that were introduced in Windows Server 2012 or earlier, but you can't manage policy settings that were introduced later, in Windows 8.1 or Windows Server 2012 R2.

If the version of the GPMC on your AGPM Server is older than the version on the computers that administrators use to manage group policy, the AGPM Server will be unable to store any policy settings that aren't available in the older version of the GPMC. For a spreadsheet of group policy settings included in Windows, see [Group Policy Settings Reference for Windows and Windows Server](https://www.microsoft.com/download/details.aspx?id=25250).

## AGPM 4.0 SP3

> [!IMPORTANT]
> AGPM v4 SP3 is the only currently supported version. For more information, see [Microsoft Desktop Optimization Pack (MDOP) support extended](/lifecycle/announcements/mdop-extended).

If you're using computers that are running Windows 11 or Windows 10 to manage GPOs, you must use AGPM 4.0 SP3. You can't install earlier versions of AGPM on computers that are running the Windows 10 operating system.

The following table lists the operating systems on which you can install AGPM 4.0 SP3, and the policy settings that you can manage by using AGPM 4.0 SP3.

| Supported configurations for the AGPM Server | Supported configurations for the AGPM Client | AGPM Support |
|--|--|--|
| Windows Server 2022, Windows Server 2019, Windows 10, or Windows 11 | Windows Server 2022, Windows Server 2019, Windows 10, or Windows 11 | Supported |
| Windows Server 2016, Windows Server 2019, Windows 10, or Windows 11 | Windows Server 2016, Windows Server 2019, Windows 10, or Windows 11 | Supported |
| Windows Server 2012 R2 | Windows 10 or Windows 11 | Supported with the caveats outlined in [Known issues managing a Windows 10 group policy client in Windows Server 2012 R2](/troubleshoot/windows-client/active-directory/known-issues-for-group-policy-clients). |
| Windows Server 2012 R2 or Windows 8.1 | Windows Server 2012 R2 or Windows 8.1 | Supported |
| Windows Server 2012 R2, Windows Server 2012, or Windows 8.1 | Windows Server 2012 or Windows 8.1 | Supported, but can't edit policy settings or preference items that exist only in Windows 8.1 |
| Windows Server 2008 R2 or Windows 7 | Windows Server 2008 R2 or Windows 7 | Supported, but can't edit policy settings or preference items that exist only in Windows 8.1 |
| Windows Server 2012, Windows Server 2008 R2, or Windows 7 | Windows Server 2008 or Windows Vista with Service Pack 1 (SP1) | Supported, but can't edit policy settings or preference items that exist only in Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 8.1, or Windows 7 |
| Windows Server 2008 or Windows Vista with SP1 | Windows Server 2012, Windows Server 2008 R2, Windows 8, or Windows 7 | Not supported |
| Windows Server 2008 or Windows Vista with SP1 | Windows Server 2008 or Windows Vista with SP1 | Supported, but can't report or edit policy settings or preference items that exist only in Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 8.1, or Windows 7 |
