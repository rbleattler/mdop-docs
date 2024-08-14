---
title: Synchronizing Office 2013 with UE-V 2.0
description: Microsoft User Experience Virtualization (UE-V) 2.0 supports the synchronization of Microsoft Office 2013 application setting using a template.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Synchronizing Office 2013 with UE-V 2.0

Microsoft User Experience Virtualization (UE-V) 2.0 supports the synchronization of Microsoft Office 2013 application setting using a template. The combination of UE-V 2 and App-V 5.0 SP2 support of Office 2013 Professional Plus enables the same experience on virtualized instance of Office 2013 from any UE-V-enabled device or virtualized desktop.

To activate UE-V application settings support of Office 2013, download the [User Experience Virtualization (UE-V) settings templates for Microsoft Office](https://www.microsoft.com/download/details.aspx?id=46367). This resource provides Microsoft-authored UE-V settings location templates.

## Microsoft Office support in UE-V

UE-V 1.0 and UE-V 2 include settings location templates for Microsoft Office 2010. These templates are distributed and registered as part of the UE-V agent installation process. These templates help synchronize users' Office experience between devices. The UE-V templates for Office 2013 provide a similar settings experience to the templates for Office 2010. Microsoft Office 2013 settings roamed by Office 365 experience aren't included in these settings. For a list of Office 365-specific settings, see [Overview of user and roaming settings for Office 2013](/previous-versions/office/office-2013-resource-kit/jj733593(v=office.15)).

## Synchronized Office 2013 settings

The following tables contain the details for Office 2013 support in UE-V:

### Supported UE-V templates for Microsoft Office

| Office 2013 templates | Office 2010 templates |
|--|--|
| MicrosoftOffice2013Win32.xml | MicrosoftOffice2010Win32.xml |
| MicrosoftOffice2013Win64.xml | MicrosoftOffice2010Win64.xml |
| MicrosoftLync2013Win32.xml | MicrosoftLync2010.xml |
| MicrosoftLync2013Win64.xml |  |

### Microsoft Office applications supported by the UE-V templates

| **Office 2013**                     | **Office 2010**                     |
|-------------------------------------|-------------------------------------|
| Microsoft Access 2013               | Microsoft Access 2010               |
| Microsoft Lync 2013                 | Microsoft Lync 2010                 |
| Microsoft Excel 2013                | Microsoft Excel 2010                |
| Microsoft InfoPath 2013             | Microsoft InfoPath 2010             |
| Microsoft OneNote 2013              | Microsoft OneNote 2010              |
| Microsoft Outlook 2013              | Microsoft Outlook 2010              |
| Microsoft PowerPoint 2013           | Microsoft PowerPoint 2010           |
| Microsoft Project 2013              | Microsoft Project 2010              |
| Microsoft Publisher 2013            | Microsoft Publisher 2010            |
| Microsoft SharePoint Designer 2013  | Microsoft SharePoint Designer 2010  |
| Microsoft Visio 2013                | Microsoft Visio 2010                |
| Microsoft Word 2013                 | Microsoft Word 2010                 |
| Microsoft Office Upload Manager     |                                     |

## Deploying the Office 2013 templates

You can deploy UE-V settings location template with the following methods:

- **Registering template via PowerShell**. If you use Windows PowerShell to manage computers, run the following Windows PowerShell command open as an administrator to register this settings location template:

    ```powershell
    Register-UevTemplate -Path <Path_to_Template>
    ```

    For more information using UE-V and Windows PowerShell, see [Managing UE-V 2.x settings location templates using Windows PowerShell and WMI](managing-ue-v-2x-settings-location-templates-using-windows-powershell-and-wmi-both-uevv2.md).

- **Registering template via template catalog path**. If you use the settings template catalog path to manage templates on users' computers, copy the Office 2013 template into the folder defined in the UE-V agent. The next time the template auto update (ApplySettingsCatalog.exe) scheduled task runs, the settings location template is registered on the device. For more information, see [Deploying the settings template catalog for UE-V 2](deploy-ue-v-2x-for-custom-applications-new-uevv2.md#deploycatalogue).

- **Registering template via Configuration Manager**. If you use Configuration Manager to manage your UE-V settings storage templates, then recreate the Template Baseline CAB, import it into Configuration Manager, and then deploy the baseline to your clients.
