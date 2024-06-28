---
title: How to Migrate Extension Points From an App-V 4.6 Package to a Converted App-V 5.1 Package for All Users on a Specific Computer
description: How to Migrate Extension Points From an App-V 4.6 Package to a Converted App-V 5.1 Package for All Users on a Specific Computer
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/21/2016
---

# How to migrate extension points from an App-V 4.6 package to a converted App-V 5.1 package for all users on a specific computer

Use the following procedure to migrate extension points from an App-V 4.6 package to an App-V 5.1 package using the deployment configuration file.

> [!NOTE]
> This procedure assumes that you are running the latest version of App-V 4.6.

The following procedure doesn't require an App-V 5.1 management server.

## Process

To migrate extension points from a package from an App-V 4.6 package to a converted App-V 5.1 package using the deployment configuration file

1. Locate the directory that contains the deployment configuration file for the package you want to migrate. To set the policy, make the following update to the `userConfiguration` section:

   `ManagingAuthority TakeoverExtensionPointsFrom46="true" PackageName=<Package ID>`

   The following is an example of content from a deployment configuration file:

    ```xml
     <?xml version="1.0" ?>
     <DeploymentConfiguration
     xmlns="<https://schemas.microsoft.com/appv/2010/deploymentconfiguration>" PackageId=<Package ID> DisplayName=<Display Name>
     <MachineConfiguration/>
     <UserConfiguration>
     <ManagingAuthority TakeoverExtensionPointsFrom46="true"
     PackageName=<Package ID>
     </UserConfiguration>
     </DeploymentConfiguration>
    ```

2. To add the App-V 5.1 package, in an elevated PowerShell command prompt type:

    ```powershell
     $pkg= Add-AppvClientPackage -Path <Path to package location> -DynamicDeploymentConfiguration <Path to the deployment configuration file>

     Publish-AppVClientPackage $pkg
    ```

3. To test the migration, open the virtual application using associated FTAs or shortcuts. The application opens with App-V 5.1. Both, the App-V 4.6 package and the converted App-V 5.1 package are published to the user, but the FTAs and shortcuts for the applications have been assumed by the App-V 5.1 package.

## Related information

[How to Revert Extension Points from an App-V 5.1 Package to an App-V 4.6 Package For All Users on a Specific Computer](how-to-revert-extension-points-from-an-app-v-51-package-to-an-app-v-46-package-for-all-users-on-a-specific-computer.md)

[Operations for App-V 5.1](operations-for-app-v-51.md)
