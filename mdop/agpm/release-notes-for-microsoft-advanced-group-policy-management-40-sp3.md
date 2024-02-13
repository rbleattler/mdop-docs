---
title: Release Notes for Microsoft Advanced Group Policy Management 4.0 SP3
description: Release Notes for Microsoft Advanced Group Policy Management 4.0 SP3
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.date: 09/27/2016
---


# Release Notes for Microsoft Advanced Group Policy Management 4.0 SP3


To search these release notes, press Ctrl+F.

Read these release notes thoroughly before you install Microsoft Advanced Group Policy Management (AGPM) 4.0 Service Pack 3 (SP3). These release notes contain information that is required to successfully install AGPM 4.0 SP3 and contain information that isn't available in the product documentation. If there's a difference between these release notes and other AGPM documentation, consider the latest change authoritative. These release notes supersede the content included with this product.

## AGPM 4.0 SP3 known issues


This section describes the known issues for AGPM 4.0 SP3.

### AGPM Client may fail to connect to the AGPM server

The AGPM client may fail to connect to the AGPM server. The error retuned to the AGPM client is 

"Text: CoCreateInstance of the client remoting object failed!

HRESULT: 0x0000000080131700"

**Workaround:** Install .NET 3.5 on the client hosting the AGPM client role.

### AGPM installation fails in Windows 10

AGPM internally enables the Windows Communication Foundation (WCF)-NonHTTP-Activation feature during installation. In Windows 10, WCF now includes a requirement to restart Windows after enabling the WCF NonHTTP-Activation feature. However, the current AGPM installer code doesn't handle this restart requirement and stops responding while it waits for the service to be activated.

**Workaround:** Before you run the AGPM installer, enable the WCF Non-HTTP Activation feature and then restart Windows.

### <a href="" id="control-panel-s--uninstall--tool-may-not-work-when-you-try-to-change-agpm-server-settings"></a>Control Panel's "Uninstall" tool may not work when you try to change AGPM Server settings

The tool in Control Panel that you use to uninstall or change a program may not work when you try to change AGPM Server settings.

**Workaround:** Before you try to change AGPM Server settings by using Control Panel, make a copy of the AGPM Archive folder. You can then use Setup.exe to reinstall the AGPM Server and choose the configuration parameters that you want.

### Reports don't display the links that were added to a Group Policy Object

The AGPM settings and difference reports don't display the links that were added to a Group Policy Object (GPO).

**Workaround:** To view the links in the reports, select the GPO in the Group Policy Management Console (GPMC), and then select the **Settings** tab in the right pane.

### Reports don't display all Choice Options Properties settings

The AGPM settings and difference reports don't display all of the settings that were selected in the **Choice Options Properties** window in the Group Policy Object Editor.

**Workaround:** Use the GPMC to view the selected **Choice Options Properties** settings in the reports.

### Reports may not display the Show and Hide tabs in certain browsers

The **Show** and **Hide** tabs, on the right side of the AGPM settings and difference reports, may not appear when you view the reports in Google Chrome or Mozilla Firefox.

**Workaround:** View the reports by using the Internet Explorer browser.

### AGPM settings and difference reports may show different content from GPMC reports

The AGPM settings and difference reports may not show the same content as reports in the GPMC.

**Workaround:** Use the GPMC to view the AGPM reports.

### AGPM Service doesn't start if the domain controller is offline

When the AGPM Service is installed on a domain controller on the Windows® 8 operating systems or later operating systems, the service doesn't start if the domain controller is offline.

**Workaround:** Manually start the AGPM Service after the domain controller is online.

### Upgrade of AGPM Server to AGPM 4.0 SP2 is blocked when you upgrade from the AGPM 4.0 release plus hotfix 1

If you try to upgrade the AGPM server to AGPM 4.0. SP2 after installing AGPM 4.0 Server and then installing the AGPM hotfix named AGPM 4.0 reports incorrect differences in the HTML report (2643502), the upgrade fails and can't be completed.

**Workaround:** Uninstall the AGPM 4.0 Server and then install AGPM 4.0 SP2.

### Reports don't display organizational unit links

If you link an uncontrolled GPO to an organizational unit and then control that GPO by using AGPM, the AGPM settings and difference reports don't display the organizational unit links.

**Workaround:** On the **Controlled** tab of the **Change Settings** node, right-click the GPO, select **Settings**, and then select **GPO Links** to view the organizational links. Alternatively, you can use the GPMC to view the links to a GPO from the **Scope** tab.

### AGPM displays an error if you select the Back button from the Change, Repair, or Remove AGPM Client dialog box

If you browse to **Programs and Features** in Control Panel and then select **Microsoft Advanced Group Policy Management - Client**, AGPM displays an error if you select **Modify** and then select the **Back** button in the **Change, Repair, or Remove AGPM Client** dialog box.

**Workaround:** Select **Cancel** to clear the error, and then start the process again. Don't select the **Back** button after you select **Modify** .

### Comment fails to appear in the History window when the Approver deploys a GPO and enters a comment

If a user who has the Editor role submits a request to deploy a GPO, and the user who has the Approver role then deploys the GPO and enters a comment, the comment fails to appear in the **History** window.

**Workaround:** None.

### Added mechanism to override AGPM default behavior of removing GPO permission changes

As of HF02, AGPM has added a registry key to enable overriding the default AGPM GPO permission behavior. For more information, please see [Changes to Group Policy object permissions through AGPM are ignored](/troubleshoot/windows-server/group-policy/changes-to-gpo-permissions-ignored).

### Take control of uncontrolled policy fails:  HRSULT: 0x80070005 (E_ACCESSDENIED)

After updating to [Microsoft Desktop Optimization Pack March 2017 Servicing Release](https://support.microsoft.com/topic/march-2017-servicing-release-for-microsoft-desktop-optimization-pack-f1c4a8d5-4af5-37f6-cb23-24fb934f416b) you may get this error. Couldn't take ownership.

**Workaround:** Check permissions of your service account on this folder: `C:\ProgramData\Microsoft\AGPM`. Make sure your service account has Full Control.

## Related information


[Advanced Group Policy Management](index.md)

[What's New in AGPM 4.0 SP3](whats-new-in-agpm-40-sp3.md)
