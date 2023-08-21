---
title: Run crash analyzer in stand-alone mode on a computer other than an end-user computer
description: How to run the crash analyzer in stand-alone mode on a computer other than an end-user computer.
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.prod: w10
ms.date: 04/20/2021
---

# How to run the crash analyzer in stand-alone mode on a computer other than an end-user computer

If you can't access the Microsoft Debugging Tools for Windows or the symbol files on the end-user computer, you can copy the dump file from the problem computer and analyze it on a computer that has the stand-alone version of Crash Analyzer installed that contains Microsoft Diagnostics and Recovery Toolset (DaRT) 10.

To run Crash Analyzer in stand-alone mode, you copy the memory dump file from the problem computer and analyze it on another computer that has the **Crash Analyzer** installed.

To run the Crash Analyzer in stand-alone mode:

1. On a computer that has DaRT 10 installed, select **Start**, type **Crash Analyzer**, and then select **Crash Analyzer**.

2. Follow the steps in the wizard, as described in [How to Run the Crash Analyzer on an End-user Computer](how-to-run-the-crash-analyzer-on-an-end-user-computer-dart-10.md).

## Related information

- [Operations for DaRT 10](operations-for-dart-10.md)
- [Diagnosing System Failures with Crash Analyzer](diagnosing-system-failures-with-crash-analyzer-dart-10.md)
- [How to Ensure that Crash Analyzer Can Access Symbol Files](how-to-ensure-that-crash-analyzer-can-access-symbol-files-dart-10.md)
