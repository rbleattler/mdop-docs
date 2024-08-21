---
title: Migrating to App-V 5.1 from a previous version
description: With Microsoft Application Virtualization (App-V) 5.1, you can migrate your existing App-V 4.6 or App-V 5.0 infrastructure to the more flexible, integrated, and easier to manage App-V 5.1 infrastructure.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Migrating to App-V 5.1 from a previous version

With Microsoft Application Virtualization (App-V) 5.1, you can migrate your existing App-V 4.6 or App-V 5.0 infrastructure to the more flexible, integrated, and easier to manage App-V 5.1 infrastructure. You can't migrate directly from App-V 4.x to App-V 5.1. If you're using App-V 4.x, you must migrate to App-V 5.0 first. For more information on migrating from App-V 4.x to App-V 5.0, see [Migrating from a previous version](migrating-from-a-previous-version-app-v-50.md)

> [!NOTE]
> App-V 5.1 packages are exactly the same as App-V 5.0 packages. There has been no change in the package format between the versions and therefore, there is no need to convert App-V 5.0 packages to App-V 5.1 packages.

For more information about the differences between App-V 4.6 and App-V 5.1, see the **Differences between App-V 4.6 and App-V 5.0 section** of [About App-V 5.0](about-app-v-50.md).

## <a href="" id="bkmk-pkgconvimprove"></a>Improvements to the App-V 5.1 package converter

You can now use the package converter to convert App-V 4.6 packages that contain scripts, and registry information and scripts from source .osd files are now included in package converter output.

You can also use the `-OSDsToIncludeInPackage` parameter with the `ConvertFrom-AppvLegacyPackage` cmdlet to specify which .osd files' information is converted and placed within the new package.

### New in App-V 5.1

New .xml files are created corresponding to the .osd files associated with a package; these files include the following information:

- Environment variables
- Shortcuts
- File type associations
- Registry information
- Scripts

You can now choose to add information from a subset of the .osd files in the source directory to the package using the `-OSDsToIncludeInPackage` parameter.

### Before App-V 5.1

Registry information and scripts included in .osd files associated with a package weren't included in package converter output. The package converter would populate the new package with information from all of the .osd files in the source directory.

### Example conversion statement

To understand the new process, review the following example `ConvertFrom-AppvLegacyPackage` package converter statement.

If the source directory (`\\OldPkgStore\ContosoApp`) includes the following files:

- ContosoApp.sft

- ContosoApp.msi

- ContosoApp.sprj

- ContosoApp\_manifest.xml

- X.osd

- Y.osd

- Z.osd

And you run this command:

```powershell
ConvertFrom-AppvLegacyPackage -SourcePath \\OldPkgStore\ContosoApp\ -DestinationPath \\NewPkgStore\ContosoApp\ -OSDsToIncludeInPackage X.osd,Y.osd
```

The following files are created in the destination directory (`\\NewPkgStore\ContosoApp`):

- ContosoApp.appv

- ContosoApp.msi

- ContosoApp\_DeploymentConfig.xml

- ContosoApp\_UserConfig.xml

- X\_Config.xml

- Y\_Config.xml

- Z\_Config.xml

#### Description of conversion to `*config.xml` files

| These source directory files | Are converted to these destination directory files | They contain these items |
|--|--|--|
| - X.osd<br>- Y.osd<br>- Z.osd | - X_Config.xml<br>- Y_Config.xml<br>- Z_Config.xml | - Environment variables<br>- Shortcuts<br>- File type associations<br>- Registry information<br>- Scripts

Each .osd file is converted to a separate, corresponding .xml file that contains the items listed here in App-V 5.1 deployment configuration format. These items can then be copied from these .xml files and placed in the deployment configuration or user configuration files as desired.

In this example, there are three .xml files, corresponding with the three .osd files in the source directory. Each .xml file contains the environment variables, shortcuts, file type associations, registry information, and scripts in its corresponding .osd file.

#### Description of conversion to user and deployment configuration files

| These source directory files | Are converted to these destination directory files | They contain these items |
|--|--|--|
| - X.osd<br>- Y.osd | - ContosoApp.appv<br>- ContosoApp_DeploymentConfig.xml<br>- ContosoApp_UserConfig.xml | - Environment variables<br>- Shortcuts<br>- File type associations |

The information from the .osd files specified in the `-OSDsToIncludeInPackage` parameter are converted and placed inside the package. The converter then populates the deployment configuration file and the user configuration file with the contents of the package, just as App-V Sequencer does when sequencing a new package.

In this example, environment variables, shortcuts, and file type associations included in X.osd and Y.osd were converted and placed in the App-V package, and some of this information was also included in the deployment configuration and user configuration files. X.osd and Y.osd were used because they were included as arguments to the `-OSDsToIncludeInPackage` parameter. No information from Z.osd was included in the package, because it wasn't included as one of these arguments.

## Converting packages created using a prior version of App-V

Use the package converter utility to upgrade virtual application packages created using versions of App-V before App-V 5.0. The package converter uses PowerShell to convert packages and can help automate the process if you have many packages that require conversion.

> [!IMPORTANT]
> After you convert an existing package, test the package before deploying it to ensure the conversion process was successful.

### What to know before you convert existing packages

| Issue | Workaround |
|--|--|
| Virtual packages using DSC aren't linked after conversion. | Link the packages using connection groups. For more information, see [Managing connection groups](managing-connection-groups51.md). |
| Environment variable conflicts are detected during conversion. | Resolve any conflicts in the associated **.osd** file. |
| Hard-coded paths are detected during conversion. | Hard-coded paths are difficult to convert correctly. The package converter detects and returns packages with files that contain hard-coded paths. View the file with the hard-coded path, and determine whether the package requires the file. If it requires the file, resequence the package. |

When converting a package check for failing files or shortcuts. Locate the item in App-V 4.6 package. It could possibly be a hard-coded path. Convert the path.

> [!NOTE]
> Use the App-V 5.1 sequencer for converting critical applications or applications that need to take advantage of features. For more information, see [How to sequence a new application with App-V 5.1](how-to-sequence-a-new-application-with-app-v-51-beta-gb18030.md).
>
> If a converted package doesn't open after you convert it, resequence the application using the App-V 5.1 sequencer.
>
> [How to convert a package created in a previous version of App-V](how-to-convert-a-package-created-in-a-previous-version-of-app-v51.md)

## Migrating clients

The following table displays the recommended method for upgrading clients.

| Task | More Information |
|--|--|
| Upgrade your environment to the latest version of App-V 4.6 | [Application Virtualization Deployment and Upgrade Considerations](../appv-v4/application-virtualization-deployment-and-upgrade-considerations-copy.md) |
| Install the App-V 5.1 client with coexistence enabled. | [How to Deploy the App-V 4.6 and the App-V 5.1 Client on the Same Computer](how-to-deploy-the-app-v-46-and-the-app-v--51-client-on-the-same-computer.md) |
| Sequence and roll out App-V 5.1 packages. As needed, unpublish App-V 4.6 packages. | [How to Sequence a New Application with App-V 5.1](how-to-sequence-a-new-application-with-app-v-51-beta-gb18030.md) |

> [!IMPORTANT]
> You must be running the latest version of App-V 4.6 to use coexistence mode. Additionally, when you sequence a package, you must configure the Managing Authority setting, which is in the **User Configuration** is located in the **User Configuration** section.

## Migrating the App-V 5.1 server full infrastructure

There's no direct method to upgrade to a full App-V 5.1 infrastructure. Use the information in the following section for information about upgrading the App-V server.

| Task | More Information |
|--|--|
| Upgrade your environment to the latest version of App-V 4.6. | [Application Virtualization Deployment and Upgrade Considerations](/previous-versions/windows/microsoft-desktop-optimization-pack/appv-v4/application-virtualization-deployment-and-upgrade-considerations-copy) |
| Deploy App-V 5.1 version of the client. | [How to Deploy the App-V Client](how-to-deploy-the-app-v-client-51gb18030.md) |
| Install App-V 5.1 server. | [How to Deploy the App-V 5.1 Server](how-to-deploy-the-app-v-51-server.md) |
| Migrate existing packages. | See the **Converting packages created using a prior version of App-V** section of this article. |

## Other migration tasks

You can also do other migration tasks such as reconfiguring end points and opening a package created using a prior version on a computer running the App-V 5.1 client. The following links provide more information about these tasks.

- [How to migrate extension points from an App-V 4.6 package to a converted App-V 5.1 package for all users on a specific computer](how-to-migrate-extension-points-from-an-app-v-46-package-to-a-converted-app-v-51-package-for-all-users-on-a-specific-computer.md)

- [How to migrate extension points from an App-V 4.6 package to App-V 5.1 for a specific user](how-to-migrate-extension-points-from-an-app-v-46-package-to-app-v-51-for-a-specific-user.md)

- [How to revert extension points from an App-V 5.1 package to an App-V 4.6 package for all users on a specific computer](how-to-revert-extension-points-from-an-app-v-51-package-to-an-app-v-46-package-for-all-users-on-a-specific-computer.md)

- [How to revert extension points from an App-V 5.1 package to an App-V 4.6 package for a specific user](how-to-revert-extension-points-from-an-app-v-51-package-to-an-app-v-46-package-for-a-specific-user.md)

## Other resources for App-V migration tasks

[Operations for App-V 5.1](operations-for-app-v-51.md)

[A simplified Microsoft App-V 5.1 management server upgrade procedure](/archive/blogs/appv/a-simplified-microsoft-app-v-5-1-management-server-upgrade-procedure)
