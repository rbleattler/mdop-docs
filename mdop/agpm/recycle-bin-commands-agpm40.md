---
title: Recycle Bin commands
description: List of Recycle Bin commands in Advanced Group Policy Management (AGPM).
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Recycle Bin commands

The **Recycle Bin** tab:

- Displays a list of group policy objects (GPOs) that were deleted from the archive.

- Provides a shortcut menu with commands for managing GPOs and for displaying reports for GPOs.

- Displays a list of the groups and users who have permission to access a selected GPO.

Right-clicking the **Group Policy Objects** list on this tab displays a shortcut menu, including whichever of the following options are applicable:

## Reports

| Command | Effect |
|--|--|
| **Settings** | Generate an HTML-based or XML-based report displaying the settings within the selected GPO or display links to the selected GPOs from organizational units as of when the GPOs were most recently controlled, imported, or checked in. |
| **Differences** | Generate an HTML-based or XML-based report comparing the settings within two selected GPOs or within the selected GPO and a template. |

## Version management

| Command | Effect |
|--|--|
| **Destroy** | Remove the selected GPO from the **Recycle Bin**, so it can no longer be restored. |
| **Restore** | Move the selected GPO from the **Recycle Bin** to the **Controlled** tab. This action doesn't restore the GPO to the production environment. |

## Miscellaneous

| Command | Effect |
|--|--|
| **Refresh** | Update the display of the Group Policy Management Console (GPMC) to incorporate any changes. Some changes aren't visible until the display is refreshed. |
| **Help** | Display help for Advanced Group Policy Management (AGPM). |

## Related articles

- [Contents tab](contents-tab-agpm40.md)

- [Performing approver tasks](performing-approver-tasks-agpm40.md)

- [Performing reviewer tasks](performing-reviewer-tasks-agpm40.md)
