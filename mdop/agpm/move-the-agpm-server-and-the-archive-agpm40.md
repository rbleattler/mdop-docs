---
title: How to move the AGPM server and the archive
description: If you replace the Advanced Group Policy Management (AGPM) server and the server on which the archive is hosted, you must move the AGPM service and the archive.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# How to move the AGPM server and the archive

If you replace the Advanced Group Policy Management (AGPM) server and the server on which the archive is hosted, you must move the AGPM service and the archive. If you prefer, you can move the AGPM service and the archive separately.

> [!NOTE]
> The AGPM server is the computer that hosts the AGPM service and the computer on which AGPM server is installed.
>
> By default, the archive is hosted on the AGPM server, but you can specify an archive path to host it on another server instead.

A user account that is a member of the Domain Admins group and has access to the previous and new AGPM servers is required to complete this procedure. Additionally, you must provide credentials for the AGPM service Account to be used by the new AGPM server to complete this procedure.

## To move the AGPM service and the archive to a different server or servers

1.  Back up the archive. For more information, see [Back up the archive](back-up-the-archive-agpm40.md).

2.  Move the AGPM service:

    1.  Stop the AGPM service. For more information, see [Start and stop the AGPM service](start-and-stop-the-agpm-service-agpm40.md).

    2.  Install AGPM server on the new server that will host the AGPM service. During this process, you specify the new archive path, the location for the archive in relation to the AGPM server. For more information, see [Step-by-step guide for Microsoft Advanced Group Policy Management 4.0](step-by-step-guide-for-microsoft-advanced-group-policy-management-40.md).

    3.  Either an AGPM administrator (full control) must configure the AGPM server connection for all group policy administrators who will use the new AGPM server and remove the connection for the old AGPM server, or else each group policy administrator must manually configure the new AGPM server connection and remove the old AGPM server connection for the AGPM snap-in on their computer. For more information, see [Configure AGPM server connections](configure-agpm-server-connections-agpm40.md).

        > [!NOTE]
        > As a best practice, you should uninstall AGPM server from the previous server. This action makes sure that the AGPM service can't be unintentionally restarted on that server. If that behavior happens, it can potentially cause confusion if any AGPM server connections to it remain.

3.  Copy the archive from the backup to the new server that will host the archive. For more information, see [Restore the archive from a backup](restore-the-archive-from-a-backup-agpm40.md).

    > [!IMPORTANT]
    > If you moved the archive without moving the AGPM service at the same time:

    1.  You must change the archive path to point to the new location for the archive in relation to the AGPM server. For more information, see [Modify the AGPM service](modify-the-agpm-service-agpm40.md).

    2.  You must re-enter and confirm the password on the **Domain Delegation** tab. For more information, see [Configure e-mail notification](configure-e-mail-notification-agpm40.md).

## Related articles

- [Back Up the archive](back-up-the-archive-agpm40.md)

- [Restore the archive from a backup](restore-the-archive-from-a-backup-agpm40.md)

- [Configure AGPM server connections](configure-agpm-server-connections-agpm40.md)

- [Modify the AGPM service](modify-the-agpm-service-agpm40.md)

- [Step-by-step guide for Microsoft Advanced Group Policy Management 4.0](step-by-step-guide-for-microsoft-advanced-group-policy-management-40.md)

- [Performing AGPM administrator tasks](performing-agpm-administrator-tasks-agpm40.md)
