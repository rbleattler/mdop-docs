---
title: How to add or upgrade packages by using the management console
description: How to add or upgrade packages by using the management console.
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.prod: w10
ms.date: 06/16/2016
---

# How to add or upgrade packages by using the management console

Use the following procedure to add or upgrade a package to the App-V 5.1 Management Console. To upgrade a package that already exists in the Management Console, use the following steps and import the upgraded package using the same package **Name**.

1. Select the **Packages** tab in the navigation pane of the Management Console display.

    The console displays the list of packages that have been added to the server along with status information about each package. When a package is selected, detailed information about the package is displayed in the **PACKAGES** pane.

    Select the **Ungrouped** drop-down list box and specify how the packages are to be displayed in the console. You can also select the associated column header to sort the packages.

2. To specify the package you want to add, select **Add or Upgrade Packages**.

3. Type the full path to the package that you want to add. Use the UNC or HTTP path format, for example `\\servername\sharename\foldername\packagename.appv` or `https://server:1234/file.appv`, and then select **Add**.

    > [!IMPORTANT]
    > You must select a package with the **.appv** file name extension.

4. The page displays the status message **Adding &lt;Packagename&gt;**. Select **IMPORT STATUS** to check the status of a package that you have imported.

    Select **OK** to add the package and close the **Add Package** page. If there was an error during the import, select **Detail** on the **Package Import** page for more information. The newly added package is now available in the **PACKAGES** pane.

5. Select **Close** to close the **Add or Upgrade Packages** page.

    **Got an App-V issue?** Use the [App-V TechNet Forum](https://social.technet.microsoft.com/Forums/home?forum=mdopappv).

## Related information

[Operations for App-V 5.1](operations-for-app-v-51.md)
