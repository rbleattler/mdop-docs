---
title: GPO commands on the controlled tab
description: List of GPO commands on the controlled tab.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# GPO commands on the controlled tab

The **Controlled** tab:

- Displays a list of group policy objects (GPOs) managed by Advanced Group Policy Management (AGPM).

- Provides a shortcut menu with commands for managing GPOs and for displaying the history and reports for GPOs.

- Displays a list of the groups and users who have permission to access a selected GPO.

Right-clicking the **Group Policy Objects** list on this tab displays a shortcut menu. This menu includes whichever of the following options are applicable.

## Control and history

| Command | Effect |
|--|--|
| **New Controlled GPO** | Create a new GPO with change control managed through AGPM and deploy it to the production environment of the domain. If you don't have permission to create a GPO, you can submit a request. (This option is displayed if no GPO is selected when right-clicking in the **Group Policy Objects** list.) |
| **History** | Open a window listing all versions of the selected GPO saved within the archive. From the history, you can obtain a report of the settings within a GPO, compare two versions of a GPO, compare a GPO to a template, or roll back to an earlier version of a GPO. |

## Reports

| Command | Effect |
|--|--|
| **Settings** | Generate an HTML-based or XML-based report that displays the settings within the selected GPO. It also displays links to the selected GPO from organizational units as of when the GPO was most recently controlled, imported, or checked in. |
| **Differences** | Generate an HTML-based or XML-based report comparing the settings within two selected GPOs or within the selected GPO and a template. |

## Editing

| Command | Effect |
|--|--|
| **Edit** | Open the **Group Policy Management Editor** window to change the selected GPO. |
| **Check Out** | Obtain a copy of the selected GPO from the archive for offline editing and prohibit anyone else from editing the GPO until it's checked back into the archive. An AGPM administrator (full control) can override the check out action. |
| **Check In** | Check the edited version of the selected GPO into the archive, so other authorized Editors can make changes or an Approver can deploy the GPO to the production environment of the domain. |
| **Undo Check Out** | Return a checked out GPO to the archive without any changes. |

## Version management

| Command | Effect |
|--|--|
| **Import from Production** | For the selected GPO, copy the version in the production environment of the domain to the archive. |
| **Import from File** | Replace the policy settings of the selected, checked-out GPO with those from a GPO backup file. |
| **Delete** | Move the selected GPO to the Recycle Bin and indicate whether to leave the deployed version (if one exists) in production or to delete the deployed version in addition to the version in the archive. If you don't have permission to delete a GPO, you're prompted to submit a request. |
| **Deploy** | Move the selected GPO that is checked into the archive to the production environment of the domain. This action makes it active on the network and overwrites the previously active version of the GPO if one existed. If you don't have permission to deploy a GPO, you can submit a request. |
| **Export to** | Save the selected GPO to a backup file so that you can copy it to another domain. |
| **Label** | Mark the selected GPO with a descriptive label and comment for record keeping. For example, "Known good." Labels appear in the **State** column and comments in the **Comment** column of the **History** window. They help you identify earlier versions of a GPO so that you can roll back if a problem occurs. |
| **Rename** | Change the name of the selected GPO. If you already deployed the GPO, the name is updated in the production environment of the domain when the GPO is redeployed. |
| **Save as Template** | Create a new template based on the settings of the selected GPO. |

## Miscellaneous

| Command | Effect |
|--|--|
| **Refresh** | Update the display of the Group Policy Management Console (GPMC) to incorporate any changes. Some changes aren't visible until the display is refreshed. |
| **Help** | Display help for AGPM. |

### Other references

- [Contents tab](contents-tab-agpm40.md)

- [Performing editor tasks](performing-editor-tasks-agpm40.md)

- [Performing approver tasks](performing-approver-tasks-agpm40.md)

- [Performing reviewer tasks](performing-reviewer-tasks-agpm40.md)
