---
title: Apply the deployment configuration file by using Windows PowerShell
description: The dynamic deployment configuration file is applied when a package is added or set to a computer running the App-V 5.1 client before the package has been published.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Apply the deployment configuration file by using Windows PowerShell

The dynamic deployment configuration file is applied when a package is added or set to a computer running the App-V 5.1 client before the package has been published. The file configures the default settings for package for all users on the computer running the App-V 5.1 client. This section describes the steps used to use a deployment configuration file. The procedure is based on the following example and assumes the following package and configuration files exist on a computer:

`c:\Packages\Contoso\MyApp.appv`

`c:\Packages\Contoso\DynamicConfigurations\deploymentconfig.xml`

## To apply the deployment configuration file using PowerShell

To specify a new default set of configurations for all users who will run the package on a specific computer, using a PowerShell console type the following:

```powershell
Add-AppVClientPackage -Path c:\Packages\Contoso\MyApp.appv -DynamicDeploymentConfiguration c:\Packages\Contoso\DynamicConfigurations\deploymentconfig.xml
```

> [!NOTE]
> This command captures the resulting object into $pkg. If the package is already present on the computer, the **Set-AppVclientPackage** cmdlet can be used to apply the deployment configuration document:
>
> ```powershell
> Set-AppVClientPackage -Name Myapp -Path c:\Packages\Contoso\MyApp.appv -DynamicDeploymentConfiguration c:\Packages\Contoso\DynamicConfigurations\deploymentconfig.xml
> ```

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)
