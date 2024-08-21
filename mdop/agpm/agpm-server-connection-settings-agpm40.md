---
title: Connection settings for AGPM server
description: You can use administrative template settings for Advanced Group Policy Management (AGPM) to centrally configure AGPM server connections for group policy administrators to whom a group policy object (GPO) with these settings is applied.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Connection settings for AGPM server

You can use administrative template settings for Advanced Group Policy Management (AGPM) to centrally configure AGPM server connections for group policy administrators to whom a group policy object (GPO) with these settings is applied.

The following settings are available under User Configuration\\Policies\\Administrative Templates\\Windows Components\\AGPM when editing a GPO.

| Setting | Effect |
|--|--|
| **AGPM: Specify default AGPM Server (all domains)** | This policy setting allows you to specify a default AGPM server for all domains. This is used only by AGPM clients, and restricts group policy administrators from connecting to another archive. You can override this default for individual domains using the **AGPM: Specify AGPM Servers** setting. |
| **AGPM: Specify AGPM Servers** | This policy setting allows you to specify the AGPM servers for individual domains. This is used only by AGPM clients, and restricts group policy administrators from connecting to a different archive for the specified domain. To specify a default AGPM server, use the **AGPM: Specify default AGPM Server (all domains)** setting and use this policy setting to override the default on a per domain basis. |

## Related articles

- [Administrative templates folder](administrative-templates-folder-agpm40.md)

- [Performing AGPM administrator tasks](performing-agpm-administrator-tasks-agpm40.md)
