---
title: Pending GPO commands
description: A list of commands for the Pending tab.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Pending GPO commands

The **Pending** tab:

- Displays a list of group policy objects (GPOs) with pending requests for GPO management actions. For example, creation, control, deployment, or deletion.

- Provides a shortcut menu with commands for responding to pending requests and for displaying the history and reports for GPOs.

- Displays a list of the groups and users who have permission to access a selected GPO.

Right-clicking the **Group Policy Objects** list on this tab displays a shortcut menu, including whichever of the following options are applicable.

## Control and history

| Command | Effect |
|--|--|
| **History** | Open a window listing all versions of the selected GPO saved within the archive. From the history, you can obtain a report of the settings within a GPO, compare two versions of a GPO, compare a GPO to a template, or roll back to an earlier version of a GPO. |
| **Withdraw** | Withdraw your pending request to create, control, or delete the selected GPO before the request is approved. |
| **Approve** | Complete a pending request from an editor to create, control, or delete the selected GPO. |
| **Reject** | Deny a pending request from an editor to create, control, or delete the selected GPO. |

## Reports

| Command | Effect |
|--|--|
| **Settings** | Generate an HTML-based or XML-based report displaying the settings within the selected GPO or display links to the selected GPOs from organizational units as of when the GPOs are most recently controlled, imported, or checked in. |
| **Differences** | Generate an HTML-based or XML-based report comparing the settings within two selected GPOs or within the selected GPO and a template. |

## Miscellaneous

| Command | Effect |
|--|--|
| **Refresh** | Update the display of the Group Policy Management Console (GPMC) to incorporate any changes. Some changes aren't visible until the display is refreshed. |
| **Help** | Display help for AGPM. |

### Related articles

- [Contents tab](contents-tab-agpm40.md)

- [Performing approver tasks](performing-approver-tasks-agpm40.md)

- [Performing reviewer tasks](performing-reviewer-tasks-agpm40.md)
