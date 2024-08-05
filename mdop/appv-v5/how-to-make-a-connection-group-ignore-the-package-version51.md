---
title: How to make a connection group ignore the package version in App-V 5.1
description: Microsoft Application Virtualization (App-V) 5.1 lets you configure a connection group to use any version of a package, which simplifies package upgrades and reduces the number of connection groups you need to create.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to make a connection group ignore the package version in App-V 5.1

Microsoft Application Virtualization (App-V) 5.1 lets you configure a connection group to use any version of a package, which simplifies package upgrades and reduces the number of connection groups you need to create.

To upgrade a package in some earlier versions of App-V, you had to perform several steps, including disabling the connection group and modifying the connection group's XML definition file.

## Task description with App-V 5.1

You can configure a connection group to accept any version of a package, which enables you to upgrade the package without having to disable the connection group.

### How the feature works

- If the connection group has access to multiple versions of a package, the latest version is used.
- If the connection group contains an optional package that has an incorrect version, the package is ignored and won't block the connection group's virtual environment from being created.
- If the connection group contains a non-optional package that has an incorrect version, the connection group's virtual environment can't be created.

## How to do the task with App-V 5.1

| Method | Steps |
|--|--|
| App-V Server - Management Console | 1. In the Management Console, select **CONNECTION GROUPS**. <br> 2. Select the correct connection group from the Connection Groups library. <br> 3. Click **EDIT** in the CONNECTED PACKAGES pane. <br> 4. Select **Use Any Version** check box next to the package name, and click **Apply**. <br> For more about adding or upgrading packages, see [How to Add or Upgrade Packages by Using the Management Console](how-to-add-or-upgrade-packages-by-using-the-management-console-51-gb18030.md). |
| App-V Client on a Stand-alone computer | 1. Create the connection group XML document. <br> 2. For the package to be upgraded, set the **Package** tag attribute **VersionID** to an asterisk (**\***). <br> 3. Use the following cmdlet to add the connection group, and include the path to the connection group XML document: <br> **Add-AppvClientConnectionGroup** <br> 4. When you upgrade a package, use the following cmdlets to remove the old package, add the upgraded package, and publish the upgraded package: <br> - RemoveAppvClientPackage <br> - Add-AppvClientPackage <br> - Publish-AppvClientPackage <br> For more information, see: <br> - The example XML file, **Connection group XML file with optional packages**, in this section: [How to Use Optional Packages in Connection Groups](how-to-use-optional-packages-in-connection-groups51.md#bkmk-apps-plugs-optional) <br> - [How to Manage App-V 5.1 Packages Running on a Stand-Alone Computer by Using PowerShell](how-to-manage-app-v-51-packages-running-on-a-stand-alone-computer-by-using-powershell.md) |

## Related articles

[Managing Connection Groups](managing-connection-groups51.md)
