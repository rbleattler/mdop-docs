---
title: How to modify App-V 5.1 client configuration using the ADMX template and group policy
description: Use the Microsoft Application Virtualization (App-V) 5.1 ADMX template to configure App-V 5.1 client settings using the ADMX Template and Group Policy.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# How to modify App-V 5.1 client configuration using the ADMX template and group policy

Use the Microsoft Application Virtualization (App-V) 5.1 ADMX template to configure App-V 5.1 client settings using the ADMX Template and Group Policy.

## To modify App-V 5.1 client configuration using group policy

1.  To modify the App-V 5.1 client configuration, locate the **ADMXTemplate** files that are available with App-V 5.1.

    > [!NOTE]
    > To download the App-V 5.1 **ADMX Templates**, see [How to Download and Deploy MDOP Group Policy (.admx) Templates](../solutions/how-to-download-and-deploy-mdop-group-policy--admx--templates.md).

2.  On the computer where you manage group policy, typically the domain controller, copy the template **.admx** file to the following directory: **&lt;Installation Drive&gt; \\ Windows \\ PolicyDefinitions**.

    Next, on the same computer, copy the **.adml** file to the following directory: **&lt;InstallationDrive&gt; \\ Windows \\ PolicyDefinitions \\ en-US**.

3.  After you have copied the files open the Group Policy Management Console, to modify the policies associated with your App-V 5.1 clients browse to **Computer Configuration** / **Policies** / **Administrative Templates** / **System** / **App-V**.

## Related topics

[App-V 5.1 Deployment Checklist](app-v-51-deployment-checklist.md)

[About Client Configuration Settings](about-client-configuration-settings51.md)
