---
title: Apply the Deployment Configuration File by Using PowerShell
description: How to Apply the Deployment Configuration File by Using PowerShell
author: aczechowski
ms.assetid: 78fe0f15-4a36-41e3-96d6-7d5aa77c1e06
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.date: 06/16/2016
---


# Apply the Deployment Configuration File by Using PowerShell


The dynamic deployment configuration file is applied when a package is added or set to a computer running the App-V 5.1 client before the package has been published. The file configures the default settings for package for all users on the computer running the App-V 5.1 client. This section describes the steps used to use a deployment configuration file. The procedure is based on the following example and assumes the following package and configuration files exist on a computer:

**c:\\Packages\\Contoso\\MyApp.appv**

**c:\\Packages\\Contoso\\DynamicConfigurations\\deploymentconfig.xml**

**To Apply the Deployment Configuration File Using PowerShell**

-   To specify a new default set of configurations for all users who will run the package on a specific computer, using a PowerShell console type the following:

    **Add-AppVClientPackage –Path c:\\Packages\\Contoso\\MyApp.appv -DynamicDeploymentConfiguration c:\\Packages\\Contoso\\DynamicConfigurations\\deploymentconfig.xml**

    **Note**
    This command captures the resulting object into $pkg. If the package is already present on the computer, the **Set-AppVclientPackage** cmdlet can be used to apply the deployment configuration document:

    **Set-AppVClientPackage –Name Myapp –Path c:\\Packages\\Contoso\\MyApp.appv -DynamicDeploymentConfiguration c:\\Packages\\Contoso\\DynamicConfigurations\\deploymentconfig.xml**



**Got an App-V issue?** Use the [App-V TechNet Forum](https://social.technet.microsoft.com/Forums/home?forum=mdopappv).

## Related topics


[Operations for App-V 5.1](operations-for-app-v-51.md)









