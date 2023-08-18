---
title: Release Notes for App-V 5.0 SP3
description: Release Notes for App-V 5.0 SP3
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.prod: w10
ms.date: 06/16/2016
---

# Release Notes for App-V 5.0 SP3

The following are known issues in Microsoft Application Virtualization (App-V) 5.0 SP3.

## Server files fail to get deleted after a new App-V 5.0 SP3 Server installation

If you uninstall the App-V 5.0 SP1 Server and then install the App-V 5.0 SP3 Server, the installation fails and the wrong version of the Management server is installed. The following errors are displayed:

`[0A5C:06F8][2014-09-12T19:08:00]i102: Detected related bundle: {bee44f0f-05be-48e4-81dd-d34a83600b95}, type: Upgrade, scope: PerMachine, version: 5.0.1218.0, operation: MajorUpgrade``[0A5C:06F8][2014-09-12T19:08:00]i000: AppvUX: A previous version of this product is installed; requesting upgrade.``[0A5C:06F8][2014-09-12T19:08:00]i102: Detected related bundle: {e1ca9d65-0ebf-4fd5-98e5-00d6453967a4}, type: Upgrade, scope: PerMachine, version: 5.0.1224.0, operation: MajorUpgrade``[0A5C:06F8][2014-09-12T19:08:00]i000: AppvUX: A previous version of this product is installed; requesting upgrade.`

The issue occurs because the Server files aren't being deleted when you uninstall App-V 5.0 SP1, so the App-V 5.0 SP3 installation process erroneously does an upgrade instead of a new installation.

**Workaround**: Delete the following registry key before you start installing App-V 5.0 SP3:

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall`

## Querying AD DS can cause some applications to work incorrectly

When you receive updated packages by querying Active Directory Domain Services for updated group memberships, it can cause some applications to work incorrectly if the applications depend on the user's access token. In addition, frequent group membership queries can cause the domain controller to overload. For more information about user access tokens, see [Access Tokens](/windows/win32/secauthz/access-tokens).

**Workaround**: Wait until the user signs out and then signs back in before you query for updated group memberships. Don't use the registry key to query for updated group memberships.

## Related information

[About App-V 5.0 SP3](about-app-v-50-sp3.md)
