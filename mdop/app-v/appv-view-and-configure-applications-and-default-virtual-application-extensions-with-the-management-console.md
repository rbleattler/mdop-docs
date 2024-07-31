---
title: How to view and configure applications and default virtual application extensions by using the management console
description: Use the following procedure to view and configure default package extensions.
author: aczechowski
ms.date: 04/19/2017
---

# How to view and configure applications and default virtual application extensions by using the management console

[!INCLUDE [Applies to Windows client versions](../includes/applies-to-windows-client-versions.md)]

Use the following procedure to view and configure default package extensions.

## To view and configure default virtual application extensions

1.  To view the package that you want to configure, open the App-V Management Console. Select the package that you want to configure, right-click the package name and select **edit default configuration**.

2.  To view the applications contained in the specified package, in the **Default Configuration** pane, click **Applications**. To view the shortcuts for that package, click **Shortcuts**. To view the file type associations for that package, click **File Types**.

3.  To enable the application extensions, select **ENABLE**.

    To enable shortcuts, select **ENABLE SHORTCUTS**. To add a new shortcut for the selected application, right-click the application in the **SHORTCUTS** pane and select **Add new shortcut**. To remove a shortcut, right-click the application in the **SHORTCUTS** pane and select **Remove Shortcut**. To edit an existing shortcut, right-click the application and select **Edit Shortcut**.

4.  To view any other application extensions, click **Advanced** and click **Export Configuration**. Type in a filename and click **Save**. You can view all application extensions associated with the package using the configuration file.

5.  To edit other application extensions, modify the configuration file and click **Import and Overwrite this Configuration**. Select the modified file and click **Open**. In the dialog box, click **Overwrite** to complete the process.

## Related articles

[Operations for App-V](appv-operations.md)
