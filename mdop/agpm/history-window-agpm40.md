---
title: History window group policy object
description: The history of a group policy object (GPO) can be displayed by double-clicking a GPO or by right-clicking a GPO and then clicking History.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# History window

The history of a group policy object (GPO) can be displayed by double-clicking a GPO or by right-clicking a GPO and then clicking **History**. It's also displayed in the Group Policy Management Console (GPMC) as a tab for each GPO. The history provides a record of events in the lifetime of the selected GPO. From the **History** window, you can obtain a report of the settings in a version of the GPO, compare multiple versions of a GPO, or roll back to an earlier version of a GPO.

## Filtering events in the History window

The tabs within the **History** window filter the states in the history of the GPO.

| Tabs | Filtering |
|--|--|
| **All States** | Display all states in the history of the GPO. |
| **Unique Versions** | Display only unique versions of the GPO checked into the archive. The version deployed to the production environment, shortcuts to unique versions, and informational states are omitted from this list. |

## Event information

Information is provided for each state in the history of the GPO.

| GPO attribute | Description |
|--|--|
| **Change Date** | Time stamp of when the action in the **State** column was performed. |
| **State** | A state in the history of the GPO. |
| **Changed By** | The person who checked in or deployed the GPO. |
| **Comment** | A comment entered by the person who checked in or deployed a GPO at the time that this version was changed, useful for identifying the specifics of the version if there's the need to roll back to an earlier version. |
| **Deletable** | Whether this version of the GPO can be deleted if the number of unique versions of each GPO retained in the archive is limited. <br> **Note:** You can change whether a version of a GPO can be deleted by right-clicking the GPO and then clicking **Do Not Allow Deletion** or **Allow Deletion**. |
| **Computer Version** | Automatically generated version of the Computer Configuration part of the GPO. |
| **User Version** | Automatically generated version of the User Configuration part of the GPO. |
| **GPO Status** | The Computer Configuration and the User Configuration can be managed separately from each other. This status shows which portions of the GPO are enabled. |
| **Source GPO Information** | For a GPO that you import from another forest, the original GPO name, domain, and user and date associated with the last change. |

## Reports

The **Settings** and **Differences** buttons display reports about GPO settings for the GPO version or versions selected. Also, right-clicking a GPO version or versions provides the option to display XML-based reports.

| Button | Effect |
|--|--|
| **Settings** | Generate an HTML-based report displaying the settings within the selected version of the GPO. |
| **Differences** | Generate an HTML-based report comparing the settings within multiple selected versions of the GPO. |

### Key to difference reports

| Symbol | Meaning | Color |
|--|--|--|
| None | Item exists with identical settings in both GPOs | Varies with level |
| `#` | Item exists in both GPOs, but with changed settings | Blue |
| `-` | Item exists only in the first GPO | Red |
| `+` | Item exists only in the second GPO | Green |

- For items with changed settings, the changed settings are identified when the item is expanded. The value for the attribute in each GPO is displayed in the same order that the GPOs are displayed in the report.

- Some changes to settings might cause an item to be reported as two items (one present only in the first GPO, one present only in the second), instead of one item that has changed.
