---
title: Release Notes for Microsoft Advanced Group Policy Management 4.0 SP1
description: Release Notes for Microsoft Advanced Group Policy Management 4.0 SP1
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---


# Release Notes for Microsoft Advanced Group Policy Management 4.0 SP1

Read these release notes thoroughly before you install Microsoft Advanced Group Policy Management (AGPM) 4.0 SP1. These release notes contain information that is required to successfully install AGPM 4.0 SP1 and contain information that isn't available in the product documentation. If there's a difference between these release notes and other AGPM documentation, the latest change should be considered authoritative. These release notes supersede the content included with this product.

## AGPM 4.0 SP1 known issues


This section contains release notes for AGPM 4.0 SP1.

### <a name="control-panel-s--uninstall--tool-may-not-work-when-you-try-to-change-agpm-server-settings"></a>Control Panel's "Uninstall" tool may not work when you try to change AGPM Server settings

The tool in Control Panel that lets you uninstall or change a program may not work when you try to change AGPM server settings.

WORKAROUND: Before you try to change AGPM server settings by using Control Panel, make a copy of the AGPM Archive folder. You can then use Setup.exe to reinstall the AGPM server and choose the configuration parameters that you want.

### Reports don't display the links that were added to a Group Policy Object

The AGPM settings and difference reports don't display the links that were added to a Group Policy Object (GPO).

WORKAROUND: To view the links in the reports, select the GPO in the Group Policy Management Console (GPMC), and select the **Settings** tab in the right pane.

### <a name="reports-do-not-display-all--choice-options-properties--settings"></a>Reports don't display all "Choice Options Properties" settings

The AGPM settings and difference reports don't display all of the settings that were selected on the Choice Options Properties window in the Group Policy Object Editor.

WORKAROUND: Use the GPMC to view the selected Choice Options Properties settings in the reports.

### Reports don't display the Show and Hide tabs in certain browsers

The Show and Hide tabs, shown on the right side of the AGPM settings and difference reports, aren't displayed when you view the reports in Google Chrome or Mozilla Firefox.

WORKAROUND: View the reports by using Internet Explorer.

### AGPM settings and difference reports may show different content from GPMC reports

The AGPM settings and difference reports may not show the same content as reports in the Group Policy Management Console (GPMC).

WORKAROUND: Use the GPMC to view the AGPM reports.

### AGPM Service doesn't start if the domain controller isn't online

When the AGPM Service is installed on a domain controller on Windows 8, the Service doesn't start if the domain controller isn't online.

WORKAROUND: Manually start the AGPM Service after the domain controller is online.

### Upgrade of AGPM Server to AGPM 4.0 SP1 is blocked when you upgrade from the AGPM 4.0 release plus the hotfix

If you try to upgrade the AGPM server to AGPM 4.0. SP1 after installing AGPM 4.0 and then installing the AGPM hotfix 2643502, the upgrade fails and can't be completed.

WORKAROUND: Uninstall the AGPM 4.0 Server and then install AGPM 4.0 SP1.

### Reports don't display organizational unit links

If you link an uncontrolled GPO to an organizational unit and then control that GPO using AGPM, the AGPM settings and difference reports don't display the organizational unit links.

WORKAROUND: From the **Controlled** tab of the **Change Settings** node, right-click the GPO and select **Settings** and then select **GPO Links** to view the organizational links. Alternatively, you can use the GPMC to view the links to a GPO from the **Scope** tab.

## Related information

[Advanced Group Policy Management](index.md)

[What's New in AGPM 4.0 SP1](whats-new-in-agpm-40-sp1.md)
