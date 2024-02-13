---
title: Deploy Microsoft Office 2010 by Using App-V
description: How to Deploy Microsoft Office 2010 by Using App-V
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---


# Deploy Microsoft Office 2010 by Using App-V


You can create Office 2010 packages for Microsoft Application Virtualization (App-V) 5.1 using one of the following methods:

-   Application Virtualization (App-V) Sequencer

-   Application Virtualization (App-V) Package Accelerator

## App-V support for Office 2010


The following table shows the App-V versions, methods of Office package creation, supported licensing, and supported deployments for Office 2010.

| Supported item | Level of support |
|--|--|
| Supported App-V versions | - 4.6<br>- 5.0<br>- 5.1 |
| Package creation | - Sequencing<br>- Package Accelerator<br>- Office Deployment Kit |
| Supported licensing | Volume Licensing |
| Supported deployments | - Desktop<br>- Personal VDI<br>- RDS |


## Creating Office 2010 App-V 5.1 using the sequencer

Sequencing Office 2010 is one of the main methods for creating an Office 2010 package on App-V 5.1.

## Creating Office 2010 App-V 5.1 packages using package accelerators


Office 2010 App-V 5.1 packages can be created through package accelerators.

For detailed instructions on how to create virtual application packages using App-V package accelerators, see [How to Create a Virtual Application Package Using an App-V Package Accelerator](how-to-create-a-virtual-application-package-using-an-app-v-package-accelerator51.md).

## Deploying the Microsoft Office package for App-V 5.1


You can deploy Office 2010 packages by using any of the following App-V deployment methods:

-   System Center Configuration Manager

-   App-V server

-   Stand-alone through PowerShell commands

## Office App-V package management and customization


Office 2010 packages can be managed like any other App-V 5.1 packages through known package management mechanisms. No special instructions are needed, for example, to add, publish, unpublish, or remove Office packages.

## Microsoft Office integration with Windows


The following table provides a full list of supported integration points for Office 2010.

| Extension Point | Description | Office 2010 |
|--|--|--|
| Lync meeting Join Plug-in for Firefox and Chrome | User can join Lync meetings from Firefox and Chrome |  |
| Sent to OneNote Print Driver | User can print to OneNote | Yes |
| OneNote Linked Notes | OneNote Linked Notes |  |
| Send to OneNote Internet Explorer Add-In | User can send to OneNote from IE |  |
| Firewall Exception for Lync and Outlook | Firewall Exception for Lync and Outlook |  |
| MAPI Client | Native apps and add-ins can interact with virtual Outlook through MAPI |  |
| SharePoint Plugin for Firefox | User can use SharePoint features in Firefox |  |
| Mail Control Panel Applet | User gets the mail control panel applet in Outlook | Yes |
| Primary Interop Assemblies | Support managed add-ins |  |
| Office Document Cache Handler | Allows Document Cache for Office applications |  |
| Outlook Protocol Search handler | User can search in Outlook | Yes |
| Active X Controls: | For more information on ActiveX controls, refer to [ActiveX Control API Reference](/previous-versions/office/developer/sharepoint-2010/ms440037(v=office.14)). |  |
| Groove.SiteClient | Active X Control |  |
| PortalConnect.PersonalSite | Active X Control |  |
| SharePoint.openDocuments | Active X Control |  |
| SharePoint.ExportDatabase | Active X Control |  |
| SharePoint.SpreadSheetLauncher | Active X Control |  |
| SharePoint.StssyncHander | Active X Control |  |
| SharePoint.DragUploadCtl | Active X Control |  |
| SharePoint.DragDownloadCtl | Active X Control |  |
| Sharpoint.OpenXMLDocuments | Active X Control |  |
| Sharepoint.ClipboardCtl | Active X Control |  |
| WinProj.Activator | Active X Control |  |
| Name.NameCtrl | Active X Control |  |
| STSUPld.CopyCtl | Active X Control |  |
| CommunicatorMeetingJoinAx.JoinManager | Active X Control |  |
| LISTNET.Listnet | Active X Control |  |
| OneDrive Pro Browser Helper | Active X Control |  |
| OneDrive Pro Icon Overlays | Windows explorer shell icon overlays when users look at folders OneDrive Pro folders |  |


## Additional resources

[Managing Connection Groups](managing-connection-groups51.md)

[About App-V 5.1 Dynamic Configuration](about-app-v-51-dynamic-configuration.md)
