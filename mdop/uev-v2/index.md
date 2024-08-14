---
title: Microsoft User Experience Virtualization (UE-V) 2.1 SP1
description: Capture and centralize your users' application settings and Windows OS settings by implementing Microsoft User Experience Virtualization (UE-V) 2.1 SP1.
author: aczechowski
manager: aaroncz
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/19/2017
---

# Microsoft User Experience Virtualization (UE-V) 2.1 SP1

[!INCLUDE [mdop-lifecycle-statement](../includes/mdop-lifecycle-statement.md)]

Capture and centralize your users' application settings and Windows OS settings by implementing Microsoft User Experience Virtualization (UE-V) 2.1 SP1. Then apply these settings to the devices users access in your organization, like desktop computers, laptops, or virtual desktop infrastructure (VDI) sessions.

With UE-V you can:

- Specify which application and desktop settings synchronize.

- Deliver the settings anytime and anywhere users work throughout the organization.

- Create custom templates for your line-of-business or non-Microsoft applications.

- Recover settings after hardware replacement or upgrade, or after reimaging a virtual machine to its initial state.

> [!NOTE]
> This documentation is a for version of UE-V that was included in the Microsoft Desktop Optimization Pack (MDOP). For information about the latest version of UE-V that's included in Windows 10 Enterprise, see [Get started with UE-V for Windows](../ue-v/uev-getting-started.md).

## Components of UE-V 2.1 SP1

This diagram shows how deployed UE-V components work together to synchronize settings.

:::image type="content" source="images/uev2archdiagram.gif" alt-text="An architectural diagram showing the components of UE-V 2, how the agent on the device interacts with the server.":::

| Component | Function |
|--|--|
| **UE-V Agent** | Installed on every computer that needs to synchronize settings, the **UE-V Agent** monitors registered applications and the operating system for any settings changes, then synchronizes those settings between computers. |
| **Settings packages** | Application settings and Windows settings are stored in **settings packages** created by the UE-V Agent. Settings packages are built, locally stored, and copied to the settings storage location. <br> - The setting values for **desktop applications** are stored when the user closes the application. <br> - Values for **Windows settings** are stored when the user signs out, when the computer is locked, or when the user disconnects remotely from a computer. <br>&nbsp; <br> The sync provider determines when the application or operating system settings are read from the **Settings Packages** and synchronized. |
| **Settings storage location** | This location is a standard network share that your users can access. The UE-V Agent verifies the location and creates a hidden system folder in which to store and retrieve user settings. |
| **Settings location templates** | UE-V uses XML files as settings location templates to monitor and synchronize desktop application settings and Windows desktop settings between user computers. By default, some settings location templates are included in UE-V. You can also create, edit, or validate custom settings location templates by [managing settings synchronization for custom applications](#customapps). <br> **Note:** Settings location templates aren't required for Windows apps. |
| **Windows app list** | Settings for Windows apps are captured and applied dynamically. The app developer specifies the settings that are synchronized for each app. UE-V determines which Windows apps are enabled for settings synchronization using a managed list of apps. By default, this list includes most Windows apps. To add or remove applications in the Windows app list, see [Managing UE-V 2.1 SP1 settings location templates using Windows PowerShell and WMI](managing-ue-v-2x-settings-location-templates-using-windows-powershell-and-wmi-both-uevv2.md). |

### <a name="customapps"></a>Managing settings synchronization for custom applications

Use these UE-V components to create and manage custom templates for your line-of-business or non-Microsoft applications.

| Component | Description |
|--|--|
| UE-V Generator | Use the **UE-V Generator** to create custom settings location templates that you can then distribute to user computers. The UE-V Generator also lets you edit an existing template or validate a template that was created by using another XML editor. |
| Settings template catalog | The **settings template catalog** is a folder path on UE-V computers or a Server Message Block (SMB) network share that stores the custom settings location templates. The UE-V Agent checks this location once a day, retrieves new or updated templates, and updates its synchronization behavior. <br> If you use only the UE-V default settings location templates, then a settings template catalog is unnecessary. For more information about settings deployment catalogs, see [Configure a UE-V settings template catalog](deploy-ue-v-2x-for-custom-applications-new-uevv2.md#deploycatalogue). |

:::image type="content" source="images/ue-vgeneratorprocess.gif" alt-text="A process diagram showing how the generator creates templates, stored in the catalog, and then used by the UE-V agent.":::

## Settings synchronized by default

UE-V synchronizes settings for these applications by default. For a complete list and more detailed information, see [Settings that are automatically synchronized in a UE-V deployment](prepare-a-ue-v-2x-deployment-new-uevv2.md#autosyncsettings).

- Microsoft Office 2013 applications

- Microsoft Office 2010 applications

- Microsoft Office 2007 applications (UE-V 2.0 only)

- Internet Explorer 8, 9, and 10

- Internet Explorer 11 in UE-V 2.1 SP1 and 2.1

- Many Windows applications, such as Xbox

- Many Windows desktop applications, such as Notepad

- Many Windows settings, such as desktop background or wallpaper

> [!NOTE]
> You can also [customize UE-V to synchronize settings](deploy-ue-v-2x-for-custom-applications-new-uevv2.md) for applications other than those synchronized by default.

## Compare UE-V to other Microsoft products

Use this table to compare UE-V to Synchronize Profiles in Windows 7, Synchronize Profiles in Windows 8, and the Sync PC Settings feature of Microsoft account.

| Feature | Synchronize profiles<br>Windows 7 | Synchronize profiles<br>Windows 8 | Synchronize profiles<br>Windows 10 | Microsoft account | UE-V 2.0 | UE-V 2.1 SP1 |
|--|--|--|--|--|--|--|
| Synchronize settings between multiple computers | X | X | X | X | X | X |
| Synchronize settings between physical and virtual apps |  |  |  |  | X | X |
| Synchronize Windows app settings |  |  | X | X | X | X |
| Manage via WMI |  | X | X |  | X | X |
| Synchronize settings changes on a regular basis |  |  |  | X | X | X |
| Minimal configuration for Setup | X | X | X | X | X | X |
| Supported on non-domain joined computers |  |  |  | X |  |  |
| Supports Primary Computer Active Directory attribute |  | X | X |  |  |  |
| Synchronizes settings between virtual desktop infrastructure (VDI)/Remote Desktop Services (RDS) and rich desktops |  |  |  |  | X | X |
| Unlimited setting storage space | X | X | X |  | X | X |
| Choice in which app settings to synchronize |  |  |  |  | X | X |
| Backup/Restore for IT Pro |  |  |  | X | Partial | X |

## UE-V 2.1 SP1 release notes

For more information, see [UE-V 2.1 SP1 release notes](microsoft-user-experience-virtualization--ue-v--21-sp1-release-notes.md).

## Other resources for this product

- [Get started with UE-V 2.1 SP1](get-started-with-ue-v-2x-new-uevv2.md)

- [Prepare a UE-V 2.1 SP1 deployment](prepare-a-ue-v-2x-deployment-new-uevv2.md)

- [Administering UE-V 2.1 SP1](administering-ue-v-2x-new-uevv2.md)

- [Technical reference for UE-V 2.1 SP1](technical-reference-for-ue-v-2x-both-uevv2.md)
