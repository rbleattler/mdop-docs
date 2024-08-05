---
title: How to customize virtual applications extensions for a specific AD group by using the management console
description: Use the following procedure to customize the virtual application extensions for an Active Directory (AD) group.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to customize virtual applications extensions for a specific AD group by using the management console

Use the following procedure to customize the virtual application extensions for an Active Directory (AD) group.

## To customize virtual applications extensions for an AD group

1.  To view the package that you want to configure, open the App-V 5.1 Management Console. To view the configuration that is assigned to a given user group, select the package, and right-click the package name and select **Edit active directory access**. Alternatively, select the package and click **EDIT** in the **AD ACCESS** pane.

2.  To customize an AD group, you can find the group from the list of **AD Entities with Access**. Then, using the drop-down box in the **Assigned Configuration** pane, select **Custom**, and then click **EDIT**.

3.  To disable all extensions for a given application, clear **ENABLE**.

    To add a new shortcut for the selected application, right-click the application in the **SHORTCUTS** pane, and select **Add new shortcut**. To remove a shortcut, right-click the application in the **SHORTCUTS** pane, and select **Remove Shortcut**. To edit an existing shortcut, right-click the application, and select **Edit Shortcut**.

4.  To view any other application extensions, click **Advanced**, and click **Export Configuration**. Type in a filename and click **Save**. You can view all application extensions that are associated with the package using the configuration file.

5.  To edit additional application extensions, modify the configuration file and click **Import and Overwrite this Configuration**. Select the modified file and click **Open**. In the dialog, click **Overwrite** to complete the process.

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)
