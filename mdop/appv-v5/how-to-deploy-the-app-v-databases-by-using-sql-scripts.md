---
title: Deploy the App-V 5.0 databases by using SQL scripts
description: How to deploy the App-V 5.0 databases by using SQL scripts.
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.prod: w10
ms.date: 06/16/2016
---

# Deploy the App-V 5.0 databases by using SQL scripts

Use the following instructions to use SQL scripts, rather than the Windows Installer, to:

- Install the App-V 5.0 databases

- Upgrade the 5.0 databases to a later version

## How to install the App-V databases by using SQL scripts

1. Before you install the database scripts, review and keep a copy of the App-V license terms. By running the database scripts, you're agreeing to the license terms. If you don't accept them, you shouldn't use this software.

2. Copy `appv_server_setup.exe` from the App-V release media to a temporary location.

3. From a command prompt, run `appv_server_setup.exe` and specify a temporary location for extracting the database scripts.

   Example: `appv_server_setup.exe /layout c:\<temporary location path>`

4. Browse to the temporary location that you created, open the extracted `DatabaseScripts` folder, and review the appropriate Readme.txt file for instructions:

    - Management database: `ManagementDatabase` subfolder

    - Reporting database: `ReportingDatabase` subfolder

## Related information

[Deploying the App-V 5.0 Server](deploying-the-app-v-50-server.md)

[How to Deploy the App-V 5.0 Server](how-to-deploy-the-app-v-50-server-50sp3.md)
