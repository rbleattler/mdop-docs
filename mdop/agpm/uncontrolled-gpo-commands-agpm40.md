---
title: Uncontrolled tab GPO commands
description: List of uncontrolled GPO commands in Advanced Group Policy Management (AGPM).
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Uncontrolled tab GPO commands

The **Uncontrolled** tab:

- Displays a list of group policy objects (GPOs) not managed by Advanced Group Policy Management (AGPM).

- Provides a shortcut menu with commands for bringing uncontrolled GPOs under the management of AGPM and for displaying the history and reports for GPOs.

- Displays a list of the groups and users who have permission to access a selected GPO.

Right-clicking the **Group Policy Objects** list on this tab displays a shortcut menu, including whichever of the following options are applicable.

## Control and history

| Command | Effect |
|--|--|
| **History** | Open a window listing all versions of the selected GPO saved within the archive. From the history, you can obtain a report of the settings within a GPO, compare two versions of a GPO, compare a GPO to a template, or roll back to an earlier version of a GPO. |
| **Control** | Bring the selected uncontrolled GPO under the change control management of AGPM. If you don't have permission to control a GPO, you're prompted to submit a request. |
| **Save as Template** | Create a new template based on the settings of the selected GPO. |

## Reports

| Command | Effect |
|--|--|
| **Settings** | Generate an HTML-based or XML-based report displaying the settings within the selected GPO. |
| **Differences** | Generate an HTML-based or XML-based report comparing the settings within two selected GPOs or within the selected GPO and a template. |

## Miscellaneous

| Command | Effect |
|--|--|
| **Refresh** | Update the display of the Group Policy Management Console (GPMC) to incorporate any changes. Some changes aren't visible until the display is refreshed. |
| **Help** | Display help for AGPM. |

## Related articles

- [Contents tab](contents-tab-agpm40.md)

- [Performing editor tasks](performing-editor-tasks-agpm40.md)

- [Performing approver tasks](performing-approver-tasks-agpm40.md)

- [Performing reviewer tasks](performing-reviewer-tasks-agpm40.md)
