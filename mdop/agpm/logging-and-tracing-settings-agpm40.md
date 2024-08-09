---
title: Settings for logging and tracing
description: The administrative template settings for Advanced Group Policy Management (AGPM) enable you to centrally configure logging and tracing options for AGPM servers and clients to which a group policy object (GPO) with these settings is applied.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Settings for logging and tracing

The administrative template settings for Advanced Group Policy Management (AGPM) enable you to centrally configure logging and tracing options for AGPM servers and clients to which a group policy object (GPO) with these settings is applied.

The following setting is available under Computer Configuration\\Policies\\Administrative Templates\\Windows Components\\AGPM when editing a GPO.

## Trace file locations

- Client: `%LocalAppData%\Microsoft\AGPM\agpm.log`

- Server: `%ProgramData%\Microsoft\AGPM\agpmserv.log`

| Setting | Effect |
|--|--|
| **AGPM: Configure logging** | This policy setting allows you to turn on and configure logging for AGPM. This setting affects both client and server components of AGPM. |

### Other articles

[Administrative templates folder](administrative-templates-folder-agpm40.md)
