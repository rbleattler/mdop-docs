---
title: Configure applications and default virtual application extensions in management console
description: How to view and configure applications and default virtual application extensions by using the management console.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 09/26/2019
---

# Configure applications and default virtual application extensions in management console

Use the following procedure to *view* and *configure* default package extensions.

## To view and configure default virtual application extensions

1.  To view the package that you want to configure, open the App-V 5.1 Management Console. Select the package that you want to configure, right-click the package name and select **edit default configuration**.

2.  To view the applications contained in the specified package, in the **Default Configuration** pane, click **Applications**. To view the shortcuts for that package, click **Shortcuts**. To view the file type associations for that package, click **File Types**.

3.  To enable the application extensions, select **ENABLE**.

    To enable shortcuts, select **ENABLE SHORTCUTS**. To add a new shortcut for the selected application, right-click the application in the **SHORTCUTS** pane and select **Add new shortcut**. To remove a shortcut, right-click the application in the **SHORTCUTS** pane and select **Remove Shortcut**. To edit an existing shortcut, right-click the application and select **Edit Shortcut**.

4.  To view any other application extensions, click **Advanced** and click **Export Configuration**. Type in a filename and click **Save**. You can view all application extensions associated with the package using the configuration file.

5.  To edit other application extensions, modify the configuration file and click **Import and Overwrite this Configuration**. Select the modified file and click **Open**. In the dialog box, click **Overwrite** to complete the process.

> [!NOTE]
> If the upload fails and the size of your configuration file is above 4MB, you will need to increase the maximum file size allowed by the server. This can be done by adding the maxRequestLength attribute with a value greater than the size of your configuration file (in KB) to the httpRuntime element on line 26 of `C:\Program Files\Microsoft Application Virtualization Server\ManagementService\Web.config`.
For example, changing `<httpRuntime targetFramework="4.5"/>` to `<httpRuntime targetFramework="4.5" maxRequestLength="8192"/>` will increase the maximum size to 8MB

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)
