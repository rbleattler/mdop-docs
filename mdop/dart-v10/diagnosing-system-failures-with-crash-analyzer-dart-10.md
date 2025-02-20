---
title: Diagnosing system failures with crash analyzer
description: Learn how to diagnose system failures with crash analyzer.
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/20/2021
---

# Diagnosing system failures with crash analyzer

The **Crash Analyzer** in Microsoft Diagnostics and Recovery Toolset (DaRT) 10 lets you debug a memory dump file on a Windows-based computer and then diagnose any related computer errors. The **Crash Analyzer** uses the Microsoft Debugging Tools for Windows to examine a memory dump file for the driver that caused the computer to fail. You can run the Crash Analyzer on an end-user computer or in stand-alone mode on a computer other than an end-user computer.

## Diagnostic tasks

- [Run the Crash Analyzer on an End-user Computer](how-to-run-the-crash-analyzer-on-an-end-user-computer-dart-10.md):

    Typically, you run **Crash Analyzer** from the **Diagnostics and Recovery Toolset** window on an end-user computer that is experiencing the problem. The **Crash Analyzer** tries to locate the Debugging Tools for Windows on the problem computer. If the directory path dialog box is empty, you must enter the location, or browse to the location of the Debugging Tools for Windows (you can download the files from Microsoft). You must also provide a path to where the symbol files are located.

    If you included the Microsoft Debugging Tools for Windows and the symbol files when you created the DaRT 10 recovery image, the Tools and symbol files should be available when you run the **Crash Analyzer** on the problem computer. If you did not include them in the DaRT recovery image, or if disk size or network connectivity problems are preventing you from obtaining them, you can alternatively run the Crash Analyzer in stand-alone mode on a computer other than the end user's computer, as described in the following section.

- [Run the Crash Analyzer in stand-alone mode on a computer other than an end user's computer](how-to-run-the-crash-analyzer-in-stand-alone-mode-on-a-computer-other-than-an-end-user-computer-dart-10.md):

    Although you typically run **Crash Analyzer** on the end-user computer that is experiencing the problem, you can also run the Crash Analyzer in stand-alone mode, on a computer other than an end-user computer. You might choose this option if you did not include the Windows Debugging Tools in the DaRT recovery image, or if disk size or network connectivity problems are preventing you from obtaining the Debugging Tools. In this case, you can copy the dump file from the problem computer and analyze it on a computer that has the stand-alone version of **Crash Analyzer** installed, such as on a help desk agent's computer.

- [Ensure that Crash Analyzer can access symbol files](how-to-ensure-that-crash-analyzer-can-access-symbol-files-dart-10.md):

    To debug applications that have stopped responding, you need access to the symbol file, which is separate from the program. Although symbol files are automatically downloaded when you run Crash Analyzer, there might be times when the problem computer does not have access to the Internet. There are several ways to ensure that you have guaranteed access to symbol files.

## Related topics

- [Operations for DaRT 10](operations-for-dart-10.md)
