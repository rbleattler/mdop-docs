---
title: Delegating access to the production environment
description: In Advanced Group Policy Management (AGPM), you can change access to group policy objects (GPOs) in the production environment of the domain, replacing any existing permissions on those GPOs.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Delegating access to the production environment

In Advanced Group Policy Management (AGPM), you can change access to group policy objects (GPOs) in the production environment of the domain, replacing any existing permissions on those GPOs. You can configure permissions at the domain level to either allow or prevent users from editing, deleting, or modifying the security of GPOs in the production environment when they aren't using the **Change Control** folder in the Group Policy Management Console (GPMC).

> [!NOTE]
>
> - Changing how access to the production environment is delegated doesn't affect users' ability to link GPOs.
> - When GPOs are controlled or deployed, access for any other accounts except those with **Read** and **Apply** permissions is removed.

A user account that has either the role of AGPM administrator (full control) or the necessary permissions in AGPM is required to complete this procedure.

## To change access to GPOs in the production environment of the domain

1. In the **Group Policy Management Console** tree, select **Change Control** in the forest and domain in which you want to manage GPOs.

2. Select the **Production Delegation** tab.

3. To add permissions for a user or group that doesn't have access to the production environment, or to replace the permissions for a user or group that does have access:

    1. Select **Add**, select a user or group, and then select **OK**.

    2. Select permissions to delegate to that user or group for the production environment, and then select **OK**.

4. To remove all permissions to the production environment for a user or group, select the user or group, select **Remove**, and then select **OK**.

## Other considerations

- By default, you must be an AGPM administrator (full control) to perform this procedure. Specifically, you must have **Modify Security** permission for the domain.

- Permissions for the AGPM Service Account can't be changed on the **Production Delegation** tab.

- By default, the following accounts have permissions for GPOs in the production environment:

    | Account | Default permissions for GPOs |
    |--|--|
    | "AGPM Service Account" | Edit settings, delete, modify security |
    | Authenticated Users | Read, apply |
    | Domain Admins | Edit settings, delete, modify security |
    | Enterprise Admins | Edit settings, delete, modify security |
    | Enterprise Domain Controllers | Read |
    | System | Edit settings, delete, modify security |

- Membership in the Group Policy Creator Owners group should be restricted, so it isn't used to circumvent AGPM management of access to GPOs. In the **Group Policy Management Console**, select **Group Policy Objects** in the forest and domain in which you want to manage GPOs, select **Delegation**, and then configure the settings to meet the needs of your organization.
