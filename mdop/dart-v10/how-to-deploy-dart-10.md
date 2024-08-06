---
title: How to deploy DaRT 10
description: The following instructions explain how to deploy Microsoft Diagnostics and Recovery Toolset (DaRT) 10 in your environment.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/20/2021
---

# How to deploy DaRT 10

The following instructions explain how to deploy Microsoft Diagnostics and Recovery Toolset (DaRT) 10 in your environment. These instructions assume that you're installing all functionality on one administrator computer. If you need to deploy or uninstall DaRT 10 on multiple computers, using an electronic software distribution system, for example, it might be easier to use command line installation options. Descriptions and examples of the available command line options are provided in this section.

> [!IMPORTANT]
> Before you install DaRT, see [DaRT 10 Supported Configurations](dart-10-supported-configurations.md) to ensure that you have installed all of the prerequisite software and that the computer meets the minimum system requirements. The computer onto which you install DaRT must be running Windows 10.

You can install DaRT using one of two different configurations:

- Install DaRT and all of its tools.

- Install only the DaRT tools that you need to create the DaRT recovery image, and then install the **Remote Connection Viewer** and, optionally, **Crash Analyzer** on a help desk computer.

The DaRT installation file is available in both x86 and x64 versions. Install the version that matches the architecture of the computer on which you're running the DaRT Recovery Image wizard, not the computer architecture of the recovery image that you're creating.

You can use either version of the DaRT installation file to create a recovery image for either x86 or x64 computers, but you can't create one recovery image for both x86 and x64 computers.

To install DaRT and all its tools on an administrator's computer:

1. Download the x86 or x64 version of the DaRT 10 installer file. Choose the architecture that matches the computer on which you're installing DaRT and running the DaRT Recovery Image wizard.

2. From the folder into which you downloaded DaRT 10, run the **MSDaRT.msi** installation file that corresponds to your system requirements.

3. On the **Welcome to the Microsoft DaRT 10 Setup Wizard** page, select **Next**.

4. Accept the Microsoft Software License Terms, and then select **Next**.

5. On the **Microsoft Update** page, select **Use Microsoft Update when I check for updates**, and then select **Next**.

6. On the **Select Installation Folder** page, select a folder, or select **Next** to install DaRT in the default installation location.

7. On the **Setup Options** page, select the DaRT features that you want to install, or select **Next** to install DaRT with all of the features.

8. To start the installation, select **Install**.

9. After the installation completes successfully, select **Finish** to exit the wizard.

## To install DaRT and all DaRT tools on an administrator's computer via command prompt

When you install or uninstall DaRT, you have the option of running the installation files at the command prompt. This section describes some examples of different options that you can specify when you install or uninstall DaRT at the command prompt.

The following example shows how to install all DaRT functionality.

```cmd
msiexec.exe /i MSDaRT.msi ADDLOCAL=CommonFiles, DaRTRecoveryImage,CrashAnalyzer,RemoteViewer
```

The following example shows how to install only the DaRT Recovery Image wizard.

```cmd
msiexec.exe /i MSDaRT.msi ADDLOCAL=CommonFiles, ,DaRTRecoveryImage
```

The following example shows how to install only the Crash Analyzer and the DaRT Remote Connection Viewer.

```cmd
msiexec.exe /i MSDaRT.msi ADDLOCAL=CommonFiles,CrashAnalyzer,RemoteViewer
```

The following example creates a setup log for the Windows Installer. This is valuable for debugging.

```cmd
msiexec.exe /i MSDaRT.msi /l*v log.txt
```

> [!NOTE]
> You can add /qn or /qb to perform a silent installation.

To validate the DaRT installation:

1. Select **Start**, and select **Diagnostics and Recovery Toolset**.

    The **Diagnostics and Recovery Toolset** window opens.

2. Check that all of the DaRT tools that you selected for installation were successfully installed.

## Related articles

- [Deploying DaRT 10 to administrator computers](deploying-dart-10-to-administrator-computers.md)
