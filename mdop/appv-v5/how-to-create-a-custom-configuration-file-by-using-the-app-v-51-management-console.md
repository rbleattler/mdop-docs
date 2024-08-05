---
title: How to create a custom configuration file by using the App-V 5.1 management console
description: You can use a dynamic configuration to customize an App-V 5.1 package for a specific user.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to create a custom configuration file by using the App-V 5.1 management console

You can use a dynamic configuration to customize an App-V 5.1 package for a specific user. However, you must first create the dynamic user configuration (.xml) file or the dynamic deployment configuration file before you can use the files. Creation of the file is an advanced manual operation. For general information about dynamic user configuration files, see, [About App-V 5.1 Dynamic Configuration](about-app-v-51-dynamic-configuration.md).

Use the following procedure to create a Dynamic User Configuration file by using the App-V 5.1 Management console.

## To create a Dynamic User Configuration file

1.  Right-click the name of the package that you want to view and select **Edit active directory access** to view the configuration that is assigned to a given user group. Alternatively, select the package, and click **Edit**.

2.  Using the list of **AD Entities with Access**, select the AD group that you want to customize. Select **Custom** from the drop-down list, if it is not already selected. A link named **Edit** will be displayed.

3.  Click **Edit**. The Dynamic User Configuration that is assigned to the AD Group will be displayed.

4.  Click **Advanced**, and then click **Export Configuration**. Type in a filename and click **Save**. Now you can edit the file to configure a package for a user.

    > [!NOTE]
    > To export a configuration while running on Windows Server, you must disable "IE Enhanced Security Configuration". If this is enabled and set to block downloads, you cannot download anything from the App-V Server.

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)
