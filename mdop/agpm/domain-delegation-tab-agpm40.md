---
title: About the domain delegation tab
description: The Domain Delegation tab on the Change Control pane provides a list of group policy administrators who have domain-level access to the archive and indicates the roles of each.
author: aczechowski
ms.assetid: 5be5841e-92fb-4af6-aa68-0ae50f8d5141
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.pagetype: mdop
ms.mktglfcycl: manage
ms.sitesec: library
ms.date: 06/16/2016
---


# About the domain delegation tab

The **Domain Delegation** tab on the **Change Control** pane provides a list of group policy administrators who have domain-level access to the archive and indicates the roles of each. Additionally, this tab enables Advanced Group Policy Management (AGPM) administrators (full control) to configure domain-level permissions for editors, approvers, reviewers, and other AGPM administrators. There are two sections on the **Domain Delegation** tab—configuration of e-mail notification and role-based delegation for AGPM at the domain level.

## Configuration of e-mail notification

The e-mail notification section of this tab identifies the approvers that receive notification when operations are pending in AGPM.

| Setting | Description |
|--|--|
| **From e-mail address** | The AGPM alias from which notification is sent to approvers. In an environment with multiple domains, this can be the same alias throughout the environment or a different alias for each domain. |
| **To e-mail address** | A comma-delimited list of e-mail addresses of approvers to whom notification is to be sent. |
| **SMTP server** | The name of the e-mail server, such as `mail.contoso.com`. |
| **User name** | A user with access to the SMTP server. |
| **Password** | User's password for authentication to the SMTP server. |
| **Confirm password** | Confirm user's password. |

## Domain-level role-based delegation

The role-based delegation section of this tab displays and enables an AGPM administrator to delegate allowed, denied, and inherited permissions for each group and user on the domain with access to the archive. An AGPM administrator can configure domain-wide permissions using either standard AGPM roles (editor, approver, reviewer, and AGPM administrator) or a customized combination of permissions for each group policy administrator.

| Button | Effect |
|--|--|
| **Add** | Add a new entry to the security descriptor. Any users or groups in Active Directory can be added as group policy administrators. |
| **Remove** | Remove the selected group policy administrators from the access control list. |
| **Properties** | Display the properties for the selected group policy administrators. |
| **Advanced** | Open the **Access Control List Editor**. |

### Other considerations

For more information about roles and permissions related to specific tasks, see the tasks in the following articles:

- [Performing AGPM administrator tasks](performing-agpm-administrator-tasks-agpm40.md)
- [Performing editor tasks](performing-editor-tasks-agpm40.md)
- [Performing approver tasks](performing-approver-tasks-agpm40.md)
- [Performing reviewer tasks](performing-reviewer-tasks-agpm40.md)

### Related articles

- [User interface: Advanced Group Policy Management](user-interface-advanced-group-policy-management-agpm40.md)

- [Performing AGPM administrator tasks](performing-agpm-administrator-tasks-agpm40.md)
