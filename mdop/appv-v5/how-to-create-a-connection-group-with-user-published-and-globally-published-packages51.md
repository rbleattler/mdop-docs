---
title: Create a connection group with user-published and globally published packages
description: You can create user-entitled connection groups that contain both user-published and globally published packages.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 11/01/2016
---

# Create a connection group with user-published and globally published packages

You can create user-entitled connection groups that contain both user-published and globally published packages, using either of the following methods:

-   [How to use PowerShell cmdlets to create the user-entitled connection groups](#bkmk-posh-userentitled-cg)

-   [How to use the App-V Server to create the user-entitled connection groups](#bkmk-appvserver-userentitled-cg)

## What to know before you start

| Unsupported scenarios and potential issues | Result |
|--|--|
| You cannot include user-published packages in globally entitled connection groups. | The connection group will fail. |
| If you publish a package globally and then create a user-published connection group in which you've made that package non-optional, you can still run `Unpublish-AppvClientPackage <package> -global` to unpublish the package, even when that package is being used in another connection group. | If any other connection groups are using that package, the package will fail in those connection groups. <br> To avoid inadvertently unpublishing a non-optional package that is being used in another connection group, we recommend that you track the connection groups in which you've used a non-optional package. |

## <a href="" id="bkmk-posh-userentitled-cg"></a> How to use PowerShell cmdlets to create user-entitled connection groups

1.  Add and publish packages by using the following commands:

    **Add-AppvClientPackage Package1\_AppV\_file\_Path**

    **Add-AppvClientPackage Package2\_AppV\_file\_Path**

    **Publish-AppvClientPackage -PackageId Package1\_ID -VersionId Package1\_Version ID -Global**

    **Publish-AppvClientPackage -PackageId Package2\_ID -VersionId Package2\_ID**

2.  Create the connection group XML file. For more information, see [About the Connection Group File](about-the-connection-group-file51.md).

3.  Add and publish the connection group by using the following commands:

    **Add-AppvClientConnectionGroup Connection\_Group\_XML\_file\_Path**

    **Enable-AppvClientConnectionGroup  -GroupId CG\_Group\_ID -VersionId CG\_Version\_ID**

## <a href="" id="bkmk-appvserver-userentitled-cg"></a> How to use the App-V Server to create user-entitled connection groups

1.  Open the App-V 5.1 Management Console.

2.  Follow the instructions in [How to Publish a Package by Using the Management Console](how-to-publish-a-package-by-using-the-management-console-51.md) to publish packages globally and to the user.

3.  Follow the instructions in [How to Create a Connection Group](how-to-create-a-connection-group51.md) to create the connection group, and add the user-published and globally published packages.

## Related topics

[Managing Connection Groups](managing-connection-groups51.md)

[How to Use Optional Packages in Connection Groups](how-to-use-optional-packages-in-connection-groups51.md)
