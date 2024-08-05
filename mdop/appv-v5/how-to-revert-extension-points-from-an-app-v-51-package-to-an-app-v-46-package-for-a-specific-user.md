---
title: How to revert extension points from an App-V 5.1 package to an App-V 4.6 package for a specific user
description: Use the following procedure to revert an App-V 5.1 package to the App-V file format using the user configuration file.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/21/2016
---

# How to revert extension points from an App-V 5.1 package to an App-V 4.6 package for a specific user

Use the following procedure to revert an App-V 5.1 package to the App-V file format using the user configuration file.

## To revert a package

1.  Ensure that App-V 4.6 package is published to the users but the FTAs and shortcuts have been assumed by App-V 5.1 package using the following migration method, [How to Migrate Extension Points From an App-V 4.6 Package to App-V 5.1 for a Specific User](how-to-migrate-extension-points-from-an-app-v-46-package-to-app-v-51-for-a-specific-user.md).

    In the **userConfiguration** section of the deployment configuration file for the converted package, to set the policy, make the following update to the **userConfiguration** section: **ManagingAuthority TakeoverExtensionPointsFrom46="false" PackageName=&lt;Package ID&gt;**

2.  From an elevated command prompt, type:

    PS&gt;**Publish-AppVClientPackage $pkg -DynamicUserConfigurationPath** &lt;path to user configuration file&gt;

3.  Perform a publishing refresh, or wait for the next scheduled publishing refresh for the App-V 4.6. Open the application using FTAs or shortcuts. The Application should now open using App-V 4.6.

    > [!NOTE]
    > If you don't need the App-V 5.1 package anymore, you can unpublish the App-V 5.1 package and the extension points will automatically revert to App-V 4.6.

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)
