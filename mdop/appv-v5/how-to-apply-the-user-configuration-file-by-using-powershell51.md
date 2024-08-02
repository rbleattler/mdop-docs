---
title: How to apply the user configuration file by using Windows PowerShell
description: The dynamic user configuration file is applied when a package is published to a specific user and determines how the package will run.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to apply the user configuration file by using Windows PowerShell

The dynamic user configuration file is applied when a package is published to a specific user and determines how the package will run.

Use the following procedure to specify a user-specific configuration file. The following procedure is based on the example:

`c:\Packages\Contoso\MyApp.appv`

## To apply a user configuration file

1.  To add the package to the computer using the PowerShell console type the following command:

    ```powershell
    Add-AppVClientPackage c:\Packages\Contoso\MyApp.appv
    ```

2.  Use the following command to publish the package to the user and specify the updated the dynamic user configuration file:

    ```powershell
    Publish-AppVClientPackage $pkg -DynamicUserConfigurationPath c:\Packages\Contoso\config.xml
    ```

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)
