---
title: Administer the AGPM server and archive checklist
description: In Advanced Group Policy Management (AGPM), AGPM administrators (full control) managed both the AGPM service and the archive.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Administer the AGPM server and archive checklist

In Advanced Group Policy Management (AGPM), AGPM administrators (full control) managed both the AGPM service and the archive. The following sections list the typical tasks for an AGPM administrator.

## Frequent tasks

- Delegate access to group policy objects (GPOs) in the archive.
  - [Delegate domain-level access to the archive](delegate-domain-level-access-to-the-archive-agpm40.md)
  - [Delegate access to an individual GPO in the archive](delegate-access-to-an-individual-gpo-in-the-archive-agpm40.md)
- Back up the archive to enable disaster recovery.
  - [Back Up the Archive](back-up-the-archive-agpm40.md)

## Infrequent tasks

- Restore the archive from a backup to recover from a disaster.
  - [Restore the Archive from a Backup](restore-the-archive-from-a-backup-agpm40.md)
- Move the AGPM Service, the archive, or both to a different server.
  - [Move the AGPM Server and the Archive](move-the-agpm-server-and-the-archive-agpm40.md)
- Change the archive path, the AGPM Service Account, or the port on which the AGPM Service listens.
  - [Modify the AGPM Service](modify-the-agpm-service-agpm40.md)
- Troubleshoot common problems with the AGPM Server.
  - [Troubleshooting AGPM](troubleshooting-agpm-agpm40.md)
  - [Configure Logging and Tracing](configure-logging-and-tracing-agpm40.md)
