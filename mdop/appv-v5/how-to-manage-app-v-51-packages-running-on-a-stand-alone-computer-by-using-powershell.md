---
title: How to manage App-V 5.1 packages running on a stand-alone computer by using Windows PowerShell
description: This article explains how to do various management tasks on a stand-alone client computer by using Windows PowerShell.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# How to manage App-V 5.1 packages running on a stand-alone computer by using Windows PowerShell

This article explains how to do various management tasks on a stand-alone client computer by using Windows PowerShell.

## <a href="" id="bkmk-return-pkgs-standalone-posh"></a>To return a list of packages

Use the following information to return a list of packages that are entitled to a specific user:

**Cmdlet**: Get-AppvClientPackage

**Parameters**: -Name -Version -PackageID -VersionID

**Example**: Get-AppvClientPackage -Name "ContosoApplication" -Version 2

## <a href="" id="bkmk-add-pkgs-standalone-posh"></a>To add a package

Use the following information to add a package to a computer.

> [!IMPORTANT]
> This example only adds a package. It does not publish the package to the user or the computer.

**Cmdlet**: Add-AppvClientPackage

**Example**: $Contoso = Add-AppvClientPackage \\\\path\\to\\appv\\package.appv

## <a href="" id="bkmk-pub-pkg-standalone-posh"></a>To publish a package

Use the following information to publish a package that has been added to a specific user or globally to any user on the computer.

| Publishing method         | Cmdlet and example                                                                 |
|---------------------------|------------------------------------------------------------------------------------|
| Publishing to the user    | **Cmdlet**: Publish-AppvClientPackage<br>**Example**: Publish-AppvClientPackage "ContosoApplication" |
| Publishing globally       | **Cmdlet**: Publish-AppvClientPackage<br>**Example**: Publish-AppvClientPackage "ContosoApplication" -Global |

## <a href="" id="bkmk-pub-pkg-a-user-standalone-posh"></a>To publish a package to a specific user

> [!NOTE]
> You must use App-V 5.0 SP2 Hotfix Package 5 or later to use this parameter.

An administrator can publish a package to a specific user by specifying the optional **-UserSID** parameter with the **Publish-AppvClientPackage** cmdlet, where **-UserSID** represents the end user's security identifier (SID).

To use this parameter:

-   You can run this cmdlet from the user or administrator session.

-   You must be logged in with administrative credentials to use the parameter.

-   The end user must be logged in.

-   You must provide the end user's security identifier (SID).

**Cmdlet**: Publish-AppvClientPackage

**Example**: Publish-AppvClientPackage "ContosoApplication" -UserSID S-1-2-34-56789012-3456789012-345678901-2345

## <a href="" id="bkmk-add-pub-pkg-standalone-posh"></a>To add and publish a package

Use the following information to add a package to a computer and publish it to the user.

**Cmdlet**: Add-AppvClientPackage

**Example**: Add-AppvClientPackage \\\\path\\to\\appv\\package.appv | Publish-AppvClientPackage

## <a href="" id="bkmk-unpub-pkg-standalone-posh"></a>To unpublish an existing package

Use the following information to unpublish a package which has been entitled to a user but not remove the package from the computer.

**Cmdlet**: Unpublish-AppvClientPackage

**Example**: Unpublish-AppvClientPackage "ContosoApplication"

## <a href="" id="bkmk-unpub-pkg-specfc-use"></a>To unpublish a package for a specific user

> [!NOTE]
> You must use App-V 5.0 SP2 Hotfix Package 5 or later to use this parameter.

An administrator can unpublish a package for a specific user by using the optional **-UserSID** parameter with the **Unpublish-AppvClientPackage** cmdlet, where **-UserSID** represents the end user's security identifier (SID).

To use this parameter:

-   You can run this cmdlet from the user or administrator session.

-   You must be logged in with administrative credentials to use the parameter.

-   The end user must be logged in.

-   You must provide the end user's security identifier (SID).

**Cmdlet**: Unpublish-AppvClientPackage

**Example**: Unpublish-AppvClientPackage "ContosoApplication" -UserSID S-1-2-34-56789012-3456789012-345678901-2345

## <a href="" id="bkmk-remove-pkg-standalone-posh"></a>To remove an existing package

Use the following information to remove a package from the computer.

**Cmdlet**: Remove-AppvClientPackage

**Example**: Remove-AppvClientPackage "ContosoApplication"

> [!NOTE]
> App-V cmdlets have been assigned to variables for the previous examples for clarity only; assignment is not a requirement. Most cmdlets can be combined as displayed in [To add and publish a package](#bkmk-add-pub-pkg-standalone-posh).

## <a href="" id="bkmk-admins-pub-pkgs"></a>To enable only administrators to publish or unpublish packages

> [!NOTE]
> This feature is supported starting in App-V 5.0 SP3.

Use the following cmdlet and parameter to enable only administrators (not end users) to publish or unpublish packages:

| Cmdlet                     | Set-AppvClientConfiguration                                                                 |
|----------------------------|---------------------------------------------------------------------------------------------|
| **Parameter**              | -RequirePublishAsAdmin                                                                       |
| **Parameter values:**      |                                                                                              |
|                            | - 0 - False                                                                                  |
|                            | - 1 - True                                                                                   |
| **Example:**               | Set-AppvClientConfiguration -RequirePublishAsAdmin 1                                         |

To use the App-V Management console to set this configuration, see [How to Publish a Package by Using the Management Console](how-to-publish-a-package-by-using-the-management-console-51.md).

## <a href="" id="bkmk-understd-pend-pkgs"></a>Understanding pending packages (UserPending and GlobalPending)

**Starting in App-V 5.0 SP2**: If you run a PowerShell cmdlet that affects a package that is currently in use, the task that you are trying to perform is placed in a pending state. For example, if you try to publish a package when an application in that package is being used, and then run **Get-AppvClientPackage**, the pending status appears in the cmdlet output as follows:

| Cmdlet output item | Description                                                                                       |
|--------------------|---------------------------------------------------------------------------------------------------|
| UserPending        | Indicates whether the listed package has a pending task that is being applied to the user:        |
|                    | - True                                                                                            |
|                    | - False                                                                                           |
| GlobalPending      | Indicates whether the listed package has a pending task that is being applied globally to the computer: |
|                    | - True                                                                                            |
|                    | - False                                                                                           |

The pending task will run later, according to the following rules:

| Task type                                           | Applicable rule                                                                 |
|-----------------------------------------------------|---------------------------------------------------------------------------------|
| User-based task, e.g., publishing a package to a user| The pending task will be performed after the user logs off and then logs back on.|
| Globally based task, e.g., enabling a connection group globally | The pending task will be performed when the computer is shut down and then restarted. |

For more information about pending tasks, see [About App-V 5.0 SP2](about-app-v-50-sp2.md#bkmk-pkg-upgr-pendg-tasks).

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)

[Administering App-V 5.1 by Using PowerShell](administering-app-v-51-by-using-powershell.md)
