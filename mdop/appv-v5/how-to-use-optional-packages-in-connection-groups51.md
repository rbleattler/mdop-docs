---
title: Use optional packages in App-V 5.1 connection groups
description: Starting in Microsoft Application Virtualization (App-V) 5.0 SP3, you can add optional packages to your connection groups to simplify connection group management.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Use optional packages in App-V 5.1 connection groups

Starting in Microsoft Application Virtualization (App-V) 5.0 SP3, you can add optional packages to your connection groups to simplify connection group management. The following table summarizes the tasks that you can complete more easily by using optional packages, and provides links to instructions for each task.

> [!NOTE]
> Optional packages aren't supported in releases prior to App-V 5.0 SP3.

Before using optional packages, see [Requirements for using optional packages in connection groups](#bkmk-reqs-using-cg).

| Link to instructions | Task |
|--|--|
| [Use one connection group, with optional packages, for multiple users who have different packages entitled to them](#bkmk-apps-plugs-optional) | Use a single connection group to make different groups of applications and plug-ins available to different users. <br> For example, you want to distribute Microsoft Office to all users, but distribute different plug-ins to different subsets of users. |
| [Unpublish or delete an optional package, or unpublish an optional package and republish it later, without changing the connection group](#bkmk-unpub-del-optl-pkg) | Unpublish, delete, or republish an optional package without having to disable, remove, edit, add, and re-enable the connection group on the App-V client. <br> You can also unpublish the optional package and republish it later without having to disable or republish the connection group. |

## <a href="" id="bkmk-reqs-using-cg"></a>Requirements for using optional packages in connection groups

Before using optional packages in connection groups, review the following requirements:

| Requirement | Details |
|--|--|
| Connection groups must contain at least one nonoptional package. | - Check carefully that you meet this requirement, as the App-V Server and the PowerShell cmdlet don't validate the requirement. <br> - If you accidentally create a connection group that doesn't contain at least one nonoptional package, and the end user tries to open a packaged application in that connection group, the connection group fails. |
| User-published connection groups can contain packages that are published globally or to the user. | - Globally published connection groups must contain only globally published packages. <br> - Globally published connection groups must contain packages that are published globally to ensure that the packages are available when starting the connection group's virtual environment. <br> - If you try to add or enable globally published connection groups that contain user-published packages, the connection group fails. |
| You must publish all nonoptional packages before publishing the connection group that contains those packages. | - A connection group's virtual environment can't start if any nonoptional packages are missing. <br> - The App-V Client fails to add or enable a connection group if any nonoptional packages aren't published. |
| Before you unpublish a globally published package, ensure that the connection groups that are entitled to all the users on that computer no longer require the package. | - The system doesn't check whether the package is part of another user's connection group. <br> - Unpublishing a global package makes it unavailable to every user on that computer, so make sure that each user's connection groups no longer contain the package, or alternatively make the package optional. |

## <a href="" id="bkmk-apps-plugs-optional"></a>Use one connection group, with optional packages, for multiple users with different packages entitled to them

You can add optional packages to connection groups, which enable you to provide different combinations of applications and plug-ins to different  users.

For example, you want to distribute Microsoft Office to your  users, but enable a certain plug-in for only a subset of users. Create a connection group that contains a package with Office, and another package with Office plug-ins. Then make the plug-ins package optional. Users who aren't entitled to the plug-in package can still run Office.

The following sections explain the steps for each method.

### Use one connection group: App-V server - management console

1. In the management console, select **CONNECTION GROUPS** to display the connection groups library.
2. Select the correct connection group from the connection groups library.
3. Select **EDIT** in the CONNECTED PACKAGES pane.
4. Select **Optional** next to the package name.
5. Select the **ADD PACKAGE ACCESS TO GROUP ACCESS** check box. This required step adds to the connection group the package entitlements that you configured earlier when you assigned packages to Active Directory groups.

### Use one connection group: App-V server - Windows PowerShell cmdlet

Use the **Add-AppvServerConnectionGroupPackage** cmdlet and specify the **-Optional** parameter:

#### Syntax

`Add-AppvServerConnectionGroupPackage [-AppvServerConnectionGroup] <SerializableConnectionGroup> [[-AppvServerPackage] <PackageVersion>] [-Optional] [-Order <int>] [-UseAnyPackageVersion]`

#### Example

`Add-AppvServerConnectionGroupPackage -Name "Connection Group 1" -PackageName "Package 1" -Optional`

### Use one connection group: App-V client on a stand-alone computer

1. Create the connection group XML document, and set the **Package** tag attribute **IsOptional** to **"true"**.
2. Use the following cmdlets to add and enable the connection group:
   - `Add-AppvClientConnectionGroup`
   - `Enable-AppvClientConnectionGroup`

#### Example connection group XML document with optional packages

```xml
<?xml version="1.0" ?>
<AppConnectionGroup
   xmlns="https://schemas.microsoft.com/appv/2014/virtualapplicationconnectiongroup"
   AppConnectionGroupId="8105CCD5-244B-4BA1-8888-E321E688D2CB"
   VersionId="84CE3797-F1CB-4475-A223-757918929EB4"
   DisplayName="Contoso Software Connection Group" >
<Packages>
<Package
   PackageId="7735d1a8-5ef9-4df9-a1cf-3aa92ef54fe7"
   VersionId="ec560d6f-e62e-48eb-a9e5-7c52a8c2e149"
   DisplayName="Contoso Business Manager"
/>

<Package
   PackageId="fc6fe0f7-be3d-4643-b37d-fc3f62d4dd5c"
   VersionId="c67a71cd-3542-4a48-93e8-20c643c50970"
   DisplayName="Contoso Forms"
   IsOptional="false"
/>
<Package
   PackageId="8f6301a5-4348-4039-9560-b27a5bb72711"
   VersionId="6c694b45-3e19-46c6-a327-d159aa39e1d2"
   DisplayName="Contoso Tax"
   IsOptional="true"
/>

<Package
   PackageId="89d701bc-d507-4299-b6b6-000000003472"
   VersionId="*"
   DisplayName="Contoso Accounts"
   IsOptional="true"
/>

</Packages>
</AppConnectionGroup>
```

## <a href="" id="bkmk-unpub-del-optl-pkg"></a>Unpublish or delete an optional package, or unpublish an optional package and republish it later, without changing the connection group

You can unpublish, delete, or republish an optional package, which is in a connection group, without having to disable or re-enable the connection group on the App-V client.

You can also unpublish an optional package and republish it later without having to disable or republish the connection group.

For example, if you publish an optional package that contains a Microsoft Office plug-in, and you want to remove the plug-in, you can unpublish the package without having to disable the connection group.

The following sections explain the steps for each method.

### Unpublish: App-V server - management console

- To unpublish the package, in the management console, select the **PACKAGES** page. Select the package that you want to unpublish, and select **Unpublish**.
- To remove an optional package from a connection group, go to the **CONNECTION GROUPS** page. Select the package that you want to remove, and select the right arrow to remove the package from the connection group pane on the bottom left.

### Unpublish: App-V client on a stand-alone computer

Use the following existing cmdlets:

- `Unpublish-AppvClientPackage`
- `Remove-AppvClientPackage`

For more information, see [How to Manage App-V 5.1 Packages Running on a Stand-Alone Computer by Using PowerShell](how-to-manage-app-v-51-packages-running-on-a-stand-alone-computer-by-using-powershell.md).

## Related articles

[Managing connection groups](managing-connection-groups51.md)
