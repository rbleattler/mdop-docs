---
title: Features on the contents tab
description: Each secondary tab within the Contents tab has two sections, Group Policy objects and Groups and Users.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Features on the contents tab

Each secondary tab within the **Contents** tab has two sections: **Group Policy objects** and **Groups and Users**.

## Group policy objects section

The **Group Policy objects** section displays a filtered list of group policy objects (GPOs) and identifies the following attributes for each GPO. You can use the **Search** box to search for GPOs with specific attributes. For more information, see [Search and filter the list of GPOs](search-and-filter-the-list-of-gpos.md).

| GPO attribute | Description |
|--|--|
| **Name** | Name of the GPO. |
| **State** | The state of the selected GPO. |
| **Changed By** | The editor who checked in or the approver who deployed the selected GPO. |
| **Change Date** | For a controlled GPO, the most recent date it was checked in after being modified or checked out to be modified. For an uncontrolled GPO, the date when it was last modified. |
| **Comment** | A comment entered by the person who checked in or deployed a GPO at the time that it was modified. Useful for identifying the specifics of the version if there's the need to roll back to an earlier version. |
| **Computer Version** | Automatically generated version of the Computer Configuration part of the GPO. |
| **User Version** | Automatically generated version of the User Configuration part of the GPO. |
| **GPO Status** | The Computer Configuration and the User Configuration can be managed separately. The GPO status indicates which portions of the GPO are enabled. |
| **WMI Filter** | Display any WMI filters that are applied to this GPO. WMI filters are managed under the **WMI Filters** folder for the domain in the console tree of the GPMC. |

## Groups and users section

When you select a GPO, the **Groups and Users** section displays a list of the groups and users with access to that GPO. It displays the allowed permissions and inheritance for each group or user. An AGPM administrator can configure permissions using either standard AGPM roles (editor, approver, reviewer, and AGPM administrator) or a customized combination of permissions.

| Button | Effect |
|--|--|
| **Add** | Add a new entry to the security descriptor. Any user or group in Active Directory can be added. |
| **Remove** | Remove the selected entry from the access control list. |
| **Properties** | Display the properties for the selected object. The properties page is the same one displayed for an object in **Active Directory Users and Computers**. |
| **Advanced** | Open the **Access Control List Editor**. |

### Other considerations

For more information about roles and permissions related to specific tasks, see the tasks in the following articles:

- [Performing AGPM administrator tasks](performing-agpm-administrator-tasks-agpm40.md)
- [Performing editor tasks](performing-editor-tasks-agpm40.md)
- [Performing approver tasks](performing-approver-tasks-agpm40.md)
- [Performing reviewer tasks](performing-reviewer-tasks-agpm40.md)
