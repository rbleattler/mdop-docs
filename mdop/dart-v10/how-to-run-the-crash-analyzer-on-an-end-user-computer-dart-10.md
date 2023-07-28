---
title: Run the crash analyzer on an end-user computer
description: How to run the crash analyzer on an end-user computer.
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.prod: w10
ms.date: 08/30/2016
---

# How to run the crash analyzer on an end-user computer

To run **Crash Analyzer** from the **Diagnostics and Recovery Toolset** window on an end-user computer that is experiencing problems, you must have the Microsoft Debugging Tools for Windows and the symbol files installed. To download the Windows Debugging Tools, see [Download debugging tools for Windows](/windows-hardware/drivers/debugger/debugger-download-tools).

To run the Crash Analyzer on an end-user computer:

1. On the **Diagnostics and Recovery Toolset** window on an end-user computer, select **Crash Analyzer**.

2. Provide the required information for the Microsoft Debugging Tools for Windows.

3. Provide the required information for the symbol files. For more information about symbol files, see [How to ensure that crash analyzer can access symbol files](how-to-ensure-that-crash-analyzer-can-access-symbol-files-dart-10.md).

4. Provide the required information for a memory dump file. To determine the location of the memory dump file:

    1. Open the **System Properties** window.

    2. Select **Start**, type **sysdm.cpl**, and then press **Enter**.

    3. Select the **Advanced** tab.

    4. In the **Startup and Recovery** area, select **Settings**.

        If you do not have access to the **System Properties** window, you can search for dump files on the end-user computer by using the **Search** tool in Microsoft Diagnostics and Recovery Toolset (DaRT) 10.

    The **Crash Analyzer** scans the memory dump file and reports a probable cause of the problem. You can view more information about the failure, such as the specific memory dump message and description, the drivers loaded at the time of the failure, and the full output of the analysis.

5. Identify the appropriate strategy to resolve the problem. The strategy may require disabling or updating the device driver that caused the failure by using the **Services and Drivers** node of the **Computer Management** tool in DaRT 10.

## Related topics

- [Diagnosing System Failures with Crash Analyzer](diagnosing-system-failures-with-crash-analyzer-dart-10.md)
- [Operations for DaRT 10](operations-for-dart-10.md)
