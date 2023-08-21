---
title: How to Plan for Using App-V with Office
description: Planning for Using App-V with Office
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.prod: w10
ms.date: 03/16/2017
---

# How to Plan for Using App-V with Office

Use the following information to plan how to deploy Office by using Microsoft Application Virtualization (App-V) 5.1. This article includes:

- [App-V support for Language Packs](#bkmk-lang-pack)

- [Supported versions of Microsoft Office](#bkmk-office-vers-supp-appv)

- [Planning for using App-V with coexisting versions of Office](#bkmk-plan-coexisting)

- [How Office integrates with Windows when you deploy use App-V to deploy Office](#bkmk-office-integration-win)

## <a name="bkmk-lang-pack"></a>App-V support for Language Packs

You can use the App-V 5.1 Sequencer to create plug-in packages for Language Packs, Language Interface Packs, Proofing Tools and ScreenTip Languages. You can then include the plug-in packages in a Connection Group, along with the Office 2013 package that you create by using the Office Deployment Toolkit. The Office applications and the plug-in Language Packs interact seamlessly in the same connection group, just like any other packages that are grouped together in a connection group.

> [!NOTE]
> Microsoft Visio and Microsoft Project don't provide support for the Thai Language Pack.

## <a name="bkmk-office-vers-supp-appv"></a>Supported versions of Microsoft Office

For a list of supported Office products, see [List of Product IDs that are supported by the Office Deployment Tool for Click-to-Run](/microsoft-365/troubleshoot/installation/product-ids-supported-office-deployment-click-to-run).

> [!NOTE]
> You must use the Office Deployment Tool to create App-V packages for Microsoft 365 Apps for enterprise. Creating packages for the volume-licensed versions of Office Professional Plus or Office Standard is not supported. You cannot use the App-V Sequencer.

## <a name="bkmk-plan-coexisting"></a>Planning for using App-V with coexisting versions of Office

You can install more than one version of Microsoft Office side by side on the same computer by using "Microsoft Office coexistence." You can implement Office coexistence with combinations of all major versions of Office and with installation methods, as applicable, by using the Windows Installer-based (MSi) version of Office, Click-to-Run, and App-V 5.1. However, using Office coexistence isn't recommended by Microsoft.

Microsoft's recommended best practice is to avoid Office coexistence completely to prevent compatibility issues. However, when you're migrating to a newer version of Office, issues occasionally arise that can't be resolved immediately, so you can temporarily implement coexistence to help facilitate a faster migration to the latest product version. Using Office coexistence on a long-term basis is never recommended, and your organization should have a plan to fully transition in the immediate future.

### Before you implement Office coexistence

Before implementing Office coexistence, review the following Office documentation. For more information, see [How to use Office 2013 suites and programs (MSI deployment) on a computer running another version of Office](/office/troubleshoot/office-suite-issues/use-multiple-versions-of-office).

The Office documentation provides extensive guidance on coexistence for Windows Installer-based (MSi) and Click-to-Run installations of Office. This App-V article on coexistence supplements the Office guidance with information that is more specific to App-V deployments.

### Supported Office coexistence scenarios

The following tables summarize the supported coexistence scenarios. They're organized according to the version and deployment method you're starting with and the version and deployment method you're migrating to. Be sure to fully test all coexistence solutions before deploying them to a production audience.

> [!NOTE]
> Microsoft doesn't support the use of multiple versions of Office in Windows Server environments that have the Remote Desktop Session Host role service enabled. To run Office coexistence scenarios, you must disable this role service.

### Windows integrations & Office coexistence

The Windows Installer-based and Click-to-Run Office installation methods integrate with certain points of the underlying Windows operating system. When you use coexistence, common operating system integrations between two Office versions can conflict, causing compatibility and user experience issues. With App-V, you can sequence certain versions of Office to exclude integrations, thereby "isolating" them from the operating system.

| Office version | Mode in which App-V can sequence this version of Office |
|--|--|
| Office 2007 | Always nonintegrated. App-V doesn't offer any operating system integrations with a virtualized version of Office 2007. |
| Office 2010 | Integrated and nonintegrated mode. |
| Office 2013 | Always integrated. Windows operating system integrations can't be disabled. |

Microsoft recommends that you deploy Office coexistence with only one integrated Office instance. For example, if you're using App-V to deploy Office 2010 and Office 2013, you should sequence Office 2010 in nonintegrated mode.

### Known limitations of Office coexistence scenarios

The following sections describe some issues that you might encounter when using App-V to implement coexistence with Office.

#### Limitations common to Windows Installer-based/Click-to-Run and App-V Office coexistence scenarios

The following limitations can occur when you install the following versions of Office on the same computer:

- Office 2010 by using the Windows Installer-based version

- Office 2013 by using App-V

After you publish Office 2013 by using App-V side by side with an earlier version of the Windows Installer-based Office 2010 might also cause the Windows Installer to start. This is because the Windows Installer-based or Click-to-Run version of Office 2010 is trying to automatically register itself to the computer.

To bypass the autoregistration operation for native Word 2010, follow these steps:

1. Exit Word 2010.

2. Start the Registry Editor by doing the following:

    - In Windows 7: Select **Start**, type **regedit** in the Start Search box, and then press Enter.

    - In Windows 8.1 or Windows 10, type **regedit** press Enter on the Start page and then press Enter.

    If you're prompted for an administrator password or for a confirmation, type the password, or select **Continue**.

3. Locate and then select the following registry subkey:

    ``` syntax
    HKEY_CURRENT_USER\Software\Microsoft\Office\14.0\Word\Options
    ```

4. On the **Edit** menu, select **New**, and then select **DWORD Value**.

5. Type **NoReReg**, and then press Enter.

6. Right-click **NoReReg** and then select **Modify**.

7. In the **Valuedata** box, type **1**, and then select **OK**.

8. On the File menu, select **Exit** to close Registry Editor.

## <a name="bkmk-office-integration-win"></a>How Office integrates with Windows when you use App-V to deploy Office

When you deploy Office 2013 by using App-V, Office is fully integrated with the operating system, which provides end users with the same features and functionality as Office has when it's deployed without App-V.

The Office 2013 App-V package supports the following integration points with the Windows operating system:

| Extension Point | Description |
|--|--|
| Lync meeting Join Plug-in for Firefox and Chrome | User can join Lync meetings from Firefox and Chrome |
| Sent to OneNote Print Driver | User can print to OneNote |
| OneNote Linked Notes | OneNote Linked Notes |
| Send to OneNote Internet Explorer Add-In | User can send to OneNote from IE |
| Firewall Exception for Lync and Outlook | Firewall Exception for Lync and Outlook |
| MAPI Client | Native apps and add-ins can interact with virtual Outlook through MAPI |
| SharePoint Plugin for Firefox | User can use SharePoint features in Firefox |
| Mail Control Panel Applet | User gets the mail control panel applet in Outlook |
| Primary Interop Assemblies | Support managed add-ins |
| Office Document Cache Handler | Allows Document Cache for Office applications |
| Outlook Protocol Search handler | User can search in Outlook |
| Active X Controls: | For more information on ActiveX controls, see [ActiveX Control API Reference](/previous-versions/office/developer/sharepoint-2010/ms440037(v=office.14)). |
| Groove.SiteClient | Active X Control |
| PortalConnect.PersonalSite | Active X Control |
| SharePoint.openDocuments | Active X Control |
| SharePoint.ExportDatabase | Active X Control |
| SharePoint.SpreadSheetLauncher | Active X Control |
| SharePoint.StssyncHander | Active X Control |
| SharePoint.DragUploadCtl | Active X Control |
| SharePoint.DragDownloadCtl | Active X Control |
| Sharpoint.OpenXMLDocuments | Active X Control |
| Sharepoint.ClipboardCtl | Active X Control |
| WinProj.Activator | Active X Control |
| Name.NameCtrl | Active X Control |
| STSUPld.CopyCtl | Active X Control |
| CommunicatorMeetingJoinAx.JoinManager | Active X Control |
| LISTNET.Listnet | Active X Control |
| OneDrive Pro Browser Helper | Active X Control |
| OneDrive Pro Icon Overlays | Windows explorer shell icon overlays when users look at folders OneDrive Pro folders |
| Shell extensions |  |
| Shortcuts |  |
| Windows search |  |
