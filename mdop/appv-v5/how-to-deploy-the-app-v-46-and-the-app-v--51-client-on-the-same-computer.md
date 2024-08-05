---
title: How to deploy the App-V 4.6 and the App-V 5.1 client on the same computer
description: Use the following information to install the Microsoft Application Virtualization (App-V) 5.1 client and the App-V 4.6 SP2 client or the App-V 4.6 S3 client on the same computer.
ms.author: aaroncz
ms.collection: must-keep
author: aczechowski
ms.date: 06/21/2016
---

# How to deploy the App-V 4.6 and the App-V 5.1 client on the same computer

Use the following information to install the Microsoft Application Virtualization (App-V) 5.1 client (preferably, with the latest Service Packs and hotfixes) and the App-V 4.6 SP2 client or the App-V 4.6 S3 client on the same computer. For supported versions, requirements, and other planning information, see [Planning for Migrating from a Previous Version of App-V](planning-for-migrating-from-a-previous-version-of-app-v51.md).

> [!WARNING]
> App-V 4.6 is no longer supported For more information, see [Microsoft Desktop Optimization Pack (MDOP) support extended](/lifecycle/announcements/mdop-extended).

## To deploy the App-V 5.1 client and App-V 4.6 client on the same computer

1.  Install the latest service pack version of the App-V client on the computer that is running App-V 4.6.

2.  Install the App-V 5.1 client on the computer that is running the App-V 4.6 SP3 version of the client. For best results, we recommend that you install all available updates to the App-V 5.1 client.

3.  Convert or re-sequence the packages gradually.

    -   To convert the packages, use the App-V 5.1 package converter and convert the required packages to the App-V 5.1 (**.appv**) file format.

    -   To re-sequence the packages, consider using the latest version of the Sequencer for best results.

    For more information about publishing packages, see [How to Publish a Package by Using the Management Console](how-to-publish-a-package-by-using-the-management-console-51.md).

4.  Deploy packages to the client computers.

5.  Convert extension points, as needed. For more information, see the following resources:

    -   [How to Migrate Extension Points From an App-V 4.6 Package to a Converted App-V 5.1 Package for All Users on a Specific Computer](how-to-migrate-extension-points-from-an-app-v-46-package-to-a-converted-app-v-51-package-for-all-users-on-a-specific-computer.md)

    -   [How to Migrate Extension Points From an App-V 4.6 Package to App-V 5.1 for a Specific User](how-to-migrate-extension-points-from-an-app-v-46-package-to-app-v-51-for-a-specific-user.md)

    -   [How to Convert a Package Created in a Previous Version of App-V](how-to-convert-a-package-created-in-a-previous-version-of-app-v51.md)

6.  Test that your App-V 5.1 packages are successful, and then remove the 4.6 packages. To check the user state of your client computers, we recommend that you use [User Experience Virtualization (UE-V)](../ue-v/uev-for-windows.md) or another user environment management tool.

## Related topics

[Planning for migrating from a previous version of App-V](planning-for-migrating-from-a-previous-version-of-app-v51.md)

[Deploying the App-V 5.1 sequencer and client](deploying-the-app-v-51-sequencer-and-client.md)
