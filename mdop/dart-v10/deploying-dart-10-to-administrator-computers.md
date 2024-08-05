---
title: Deploying DaRT 10 to administrator computers
description: Before you begin the deployment of Microsoft Diagnostics and Recovery Toolset (DaRT) 10, review the requirements for your environment.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/20/2021
---

# Deploying DaRT 10 to administrator computers

Before you begin the deployment of Microsoft Diagnostics and Recovery Toolset (DaRT) 10, review the requirements for your environment. This includes the hardware requirements for installing DaRT 10. For more information about DaRT hardware and software requirements, see [DaRT 10 Supported Configurations](dart-10-supported-configurations.md).

## Deployment information

The topics in this section can be used to help you deploy DaRT in your enterprise based on your environment and deployment strategy.

- [Deploy DaRT 10](how-to-deploy-dart-10.md):

    You can use the Windows Installer file for DaRT to install DaRT on a computer that you will use to first create the DaRT recovery image and then troubleshoot and fix end-user computers. Frequently, across an organization, you might install on the administrator computer only the DaRT functionality that you need to create a DaRT recovery image. Then, on a help desk administrator's computer, you might install only the DaRT functionality that you must have to troubleshoot a problem computer, such as the DaRT Remote Connection Viewer and the Crash Analyzer.

    In addition to manually running the Windows Installer file to install DaRT, you can also install DaRT at the command prompt to support enterprise software deployment systems such as System Center Configuration Manager 2012.

- [Change, repair, or remove DaRT 10](how-to-change-repair-or-remove-dart-10.md):

    You can change, repair, or remove the DaRT installation by double-clicking the DaRT installation file and then clicking the button that corresponds to the action that you want to perform or through the Windows Control Panel.
