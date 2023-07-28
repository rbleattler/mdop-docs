---
title: Microsoft User Experience Virtualization (UE-V) 2.1 Release Notes
description: Microsoft User Experience Virtualization (UE-V) 2.1 Release Notes
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.prod: w10
ms.date: 08/30/2016
---

# Microsoft User Experience Virtualization (UE-V) 2.1 Release Notes

You should read these release notes thoroughly before you install UE-V. The release notes contain information that is required to successfully install User Experience Virtualization, and contain additional information that isn't available in the product documentation. If there are differences between these release notes and other UE-V documentation, the latest change should be considered authoritative. These release notes supersede the content that is included with this product.

## UE-V known issues


This section contains release notes for User Experience Virtualization.

### UE-V settings location templates for Skype cause Skype to crash

When a user generates a valid settings location template for the Skype desktop application, registers it, and then launches the Skype desktop application, Skype crashes. An ACCESS\_VIOLATION is recorded in the Application Event Log.

WORKAROUND: Remove or unregister the Skype template to allow Skype to work again.

### Existing scripts for silent installations of UE-V may fail

Two changes made to the UE-V installer can cause silent installation scripts that worked for previous versions of UE-V to fail when installing UE-V 2.1. The first is a new requirement that users must accept the license terms and agree to or decline participation in the Customer Experience Improvement Program (CEIP), even during a silent installation. Using the /q parameter is no longer sufficient to indicate acceptance of the license terms and agreement to participate in CEIP.

Second, the installer now forces a computer restart after installing the UE-V Agent. This can cause an install script to fail if it isn't expecting the restart (for example, it installs the UE-V Agent first and then immediately installs the generator).

WORKAROUND: The UE-V installer (.msi) has two new command-line parameters that support silent installations.

| Parameter | Description |
|--|--|
| `/ACCEPTLICENSETERMS=True` | Set this parameter to **True** to install UE-V silently. Adding this parameter implies that the user accepts the UE-V license terms, which are found by default at the following path: `%ProgramFiles%\Microsoft User Experience Virtualization\Agent` |
| `/NORESTART` | This parameter prevents the mandatory restart after the UE-V agent is installed. A return code of 3010 indicates that a restart is required prior to using UE-V. |

### Registry settings don't synchronize between App-V and native applications on the same computer

When a computer has an application that is installed through both Application Virtualization (App-V) and locally with a Windows Installer (.msi) file, the registry-based settings don't synchronize between the technologies.

WORKAROUND: To resolve this problem, run the application by selecting one of the two technologies, but not both.

### Unpredictable results with both Office 2010 and Office 2013 installed

When a user has both Office 2010 and Office 2013 installed, any common settings between the two versions of Office are roamed by UE-V. This could cause the Office 2010 package size to be large or result in unpredictable conflicts with 2013, particularly if Office 365 is used.

WORKAROUND: Install only one version of Office or limit which settings are synchronized by UE-V.

### Uninstall and reinstall of Windows 8 app reverts settings to initial state

While using UE-V settings synchronization for a Windows 8 app, if the user uninstalls the app and then reinstalls the app, the app's settings revert to their default values.  This happens because the uninstall removes the local (cached) copy of the app's settings but doesn't remove the local UE-V settings package.  When the app is reinstalled and launched, UE-V gathers the app settings that were reset to the app defaults and then uploads the default settings to the central storage location.  Other computers running the app then download the default settings.  This behavior is identical to the behavior of desktop applications.

WORKAROUND: None.

### UE-V doesn't support roaming settings between 32-bit and 64-bit versions of Microsoft Office

We recommend that you install the 32-bit version of Microsoft Office for both 32-bit and 64-bit operating systems. To choose the Microsoft Office version that you need, see [Choose between the 64-bit or 32-bit version of Office](https://support.microsoft.com/office/choose-between-the-64-bit-or-32-bit-version-of-office-2dee7807-8f95-4d0c-b5fe-6c6f49b8d261). UE-V supports roaming settings between identical architecture versions of Office. For example, 32-bit Office settings will roam between all 32-bit Office instances. UE-V doesn't support roaming settings between 32-bit and 64-bit versions of Office.

WORKAROUND: None

### MSI files aren't localized

UE-V 2.0 includes a localized setup program for both the UE-V Agent and UE-V generator. These MSI files are still available but the user interface is minimized and the MSI files only display in English. Despite the file being in English, the setup program installs all supported languages during the installation.

WORKAROUND: None

### Favicons that are associated with Internet Explorer 9 favorites don't roam

The favicons that are associated with Internet Explorer 9 favorites aren't roamed by User Experience Virtualization and don't appear when the favorites first appear on a new computer.

WORKAROUND: Favicons will appear with their associated favorites once the bookmark is used and cached in the Internet Explorer 9 browser.

### File settings paths are stored in registry

Some application settings store the paths of their configuration and settings files as values in the registry. The files that are referenced as paths in the registry must be synchronized when settings are roamed between computers.

WORKAROUND: Use folder redirection or some other technology to ensure that any files that are referenced as file settings paths are present and placed in the same location on all computers where settings roam.

### Long Settings Storage Paths could cause an error

Keep settings storage paths as short as possible. Long paths could prevent resolution or synchronization. UE-V uses the Settings storage path as part of the calculated path to store settings. That path is calculated in the following way: settings storage path + `settingspackages` + package dir (template ID) + package name (template ID) + `.pkgx`. If that calculated path exceeds 260 characters, package storage will fail and generate the following error message in the UE-V operational event log:

`[boost::filesystem::copy_file: The system cannot find the path specified]`

To check the operational log events, open the Event Viewer and navigate to Applications and Services Logs / Microsoft / User Experience Virtualization / Logging / Operational.

WORKAROUND: None.

### Some operating system settings only roam between like operating system versions

Operating system settings for Narrator and currency characters specific to the locale (that is, language and regional settings)  only roam across like operating system versions of Windows. For example, currency characters won't roam between Windows 7 and Windows 8.

WORKAROUND: None

### UE-V 1 agent generates errors when running UE-V 2 templates

If a UE-V 2 settings location template is distributed to a computer installed with a UE-V 1 agent, some settings fail to synchronize between computers and the agent reports errors in the event log.

WORKAROUND: When migrating from UE-V 1 to UE-V 2 and it's likely you'll have computers running the previous version of the agent, create a separate UE-V 2.0 catalog to support the UE-V 2.0 Agent and templates.

## Hotfixes and Knowledge Base articles for UE-V 2.1


This section contains hotfixes and KB articles for UE-V 2.1.

- 3018608: UE-V 2.1 - TemplateConsole.exe crashes when UE-V WMI classes are missing

- 2903501: UE-V: User Experience Virtualization (UE-V) compatibility with user profiles

- 2770042: [UE-V Registry Settings](/troubleshoot/windows-client/ue-v/ue-v-registry-settings)

- 2847017: UE-V settings replicated by Internet Explorer

- 2769631: How to repair a corrupted UE-V install

- 2850989: Migrating MAPI profiles with Microsoft UE-V isn't supported

- 2769586: UE-V roams empty folders and registry keys

- 2782997: [How To Enable Debug Logging in Microsoft User Experience Virtualization (UE-V)](/troubleshoot/windows-client/ue-v/enable-debug-logging)

- 2769570: UE-V doesn't update the theme on RDS or VDI sessions

- 2850582: How To Use Microsoft User Experience Virtualization With App-V Applications

- 3041879: Current file versions for Microsoft User Experience Virtualization

- 2843592: Information on User Experience Virtualization and High Availability
