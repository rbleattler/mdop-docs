---
title: Commands on the Templates tab
description: List of commands on the Templates tab.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Commands on the Templates tab

The **Templates** tab:

- Displays a list of available templates that you can use to create new group policy objects (GPOs).

- Provides a shortcut menu with commands for creating a GPO based on a selected template, managing templates, and displaying reports for templates.

- Displays a list of the groups and users who have permission to access a selected template.

Because a template can't be altered, templates have no history. However, like any GPO version, the settings of a template can be displayed with a settings report or compared to another GPO with a difference report.

> [!NOTE]
> A template is an uneditable, static version of a GPO for use as a starting point for creating new, editable GPOs.

Right-clicking the **Group Policy Objects** list on this tab displays a shortcut menu, including whichever of the following options are applicable.

## Control

| Command | Effect |
|--|--|
| **New Controlled GPO** | Create a new GPO based on the selected template. The option to deploy the new GPO to the production environment of the domain is provided. If you don't have permission to create a GPO, you're prompted to submit a request. This option is displayed if no GPO is selected when right-clicking in the **Group Policy Objects** list. |

## Reports

| Command | Effect |
|--|--|
| **Settings** | Generate an HTML-based or XML-based report displaying the settings within the selected GPO. |
| **Differences** | Generate an HTML-based or XML-based report comparing the settings within two selected GPO templates. |

## Template management

| Command | Effect |
|--|--|
| **Set as Default** | Set the selected template as the default to be used automatically when creating a new GPO. |
| **Delete** | Move the selected template to the **Recycle Bin**. If you don't have permission to delete a GPO, you're prompted to submit a request. |
| **Rename** | Change the name of the selected template. |

## Miscellaneous

| Command | Effect |
|--|--|
| **Refresh** | Update the display of the Group Policy Management Console to incorporate any changes. Some changes aren't visible until the display is refreshed. |
| **Help** | Display help for Advanced Group Policy Management (AGPM). |

### Related articles

- [Contents tab](contents-tab-agpm40.md)

- [Performing editor tasks](performing-editor-tasks-agpm40.md)

- [Performing reviewer tasks](performing-reviewer-tasks-agpm40.md)
