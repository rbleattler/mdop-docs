---
title: Import an application
description: How to import an application
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.prod: w10
ms.date: 06/16/2016
---

# Import an application

Typically, you import applications to make them available to stream from an Application Virtualization Management Server. You can also add an application manually, but you must provide precise, detailed information about the application to do so. For more information, see [How to Manually Add an Application](how-to-manually-add-an-application.md).

> [!NOTE]
> To import an application, you must have its sequenced Open Software Descriptor (OSD) file or its Sequencer Project (SPRJ) file available on the server.

When importing an application, you should make sure the server is configured with a value in the **Default Content Path** field on the **General** tab of the **System Options** dialog (accessible by right-clicking the **Application Virtualization System** node in the App-V Server Console). The default content path value defines where the applications will be imported, and during the import process, this value is used to modify the paths defined in the OSD file for the SFT file and for the icon shortcuts. In the OSD file, the path for the SFT file is specified in the CODEBASE HREF entry and the path for the icons is specified in the SHORTCUTS entry.

During the import process, the protocol, server, and, if present, port specified in these two paths in the OSD file will be replaced with the value from the default content path. The following table provides an example of how the import path will be affected.

| Default Content Path | OSD File CODEBASE HREF | Resulting Value |
|--|--|--|
| `\server\content` | `https://WebServer/myFolder/package.sft` | `\server\content\myFolder\package.sft` |

## To import an application

1. Right-click the **Applications** node in the left pane, and choose **Import Applications**.

2. In the **Open** dialog box, navigate to the application's SPRJ or OSD file. Highlight the file and select **Open**.

3. In the **New Application Wizard**, be sure the **Enabled** box is selected for applications you want to stream. There you can also enter a description and verify the server and file paths. Also, if you have set up license and server groups, you can select those.

4. Select **Next**.

5. On the **Published Shortcuts** screen, select the boxes for the locations where you would like the application shortcuts to appear on the client computers.

6. Select **Next**.

7. In the **File Associations** screen, you can add new file associations to this application. To do so, select **Add**, enter the extension (without a preceding dot), enter a description, and select **OK**.

    > [!NOTE]
    > Applications sequenced with Sequencer 4.0 populate the **File Associations** dialog box when you import or create them through the management console. Applications with previous Sequencer version packages do not.

8. Select **Next**.

9. In the **Access Permissions** screen, select **Add**.

10. Complete the **Select Groups** dialog box. When you finish, select **OK**.

11. Select **Next**.

12. On the **Summary** screen, you can review the import settings. Select **Finish**, or select **Back** to change the import or select **Cancel** to cancel the import.

## Related information

[How to Manage Application Groups in the Server Management Console](how-to-manage-application-groups-in-the-server-management-console.md)

[How to Manage Applications in the Server Management Console](how-to-manage-applications-in-the-server-management-console.md)

[How to Manually Add an Application](how-to-manually-add-an-application.md)
