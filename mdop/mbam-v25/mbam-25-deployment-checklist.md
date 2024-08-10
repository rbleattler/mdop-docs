---
title: MBAM 2.5 deployment checklist
description: You can use this checklist to help you during Microsoft BitLocker Administration and Monitoring (MBAM) deployment with a stand-alone topology.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# MBAM 2.5 deployment checklist

You can use this checklist to help you during Microsoft BitLocker Administration and Monitoring (MBAM) deployment with a stand-alone topology.

> [!NOTE]
> This checklist outlines the recommended steps and a high-level list of items to consider when you deploy Microsoft BitLocker Administration and Monitoring features. We recommend that you copy this checklist into a spreadsheet program and customize it for your use.

|Check| Task | References | Notes |
|--|--|--|--|
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | Review and complete all planning steps to prepare your environment for MBAM deployment. | [MBAM 2.5 Planning Checklist](mbam-25-planning-checklist.md) |  |
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | Review the supported configurations information to ensure that MBAM supports the selected client and server computers. | [MBAM 2.5 Supported Configurations](mbam-25-supported-configurations.md) |  |
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | Install the MBAM Server software. | [Installing the MBAM 2.5 Server Software](installing-the-mbam-25-server-software.md) |  |
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | Configure the MBAM Server features: | [Configuring the MBAM 2.5 Server Features](configuring-the-mbam-25-server-features.md) |  |
|  | - Compliance and Audit Database and Recovery Database |  |  |
|  | - Reports |  |  |
|  | - Web applications |  |  |
|  | - Configuration Manager Integration topology (needed only if you run MBAM with this topology) |  |  |
|  | **Note:** Note the names of the servers on which you configure each feature. You'll use this information throughout the configuration process. |  |  |
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | Validate the MBAM configuration. | [Validating the MBAM 2.5 Server Feature Configuration](validating-the-mbam-25-server-feature-configuration.md) |  |
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | Copy the MBAM Group Policy Template and edit the Group Policy settings. | [Copying the MBAM 2.5 Group Policy Templates](copying-the-mbam-25-group-policy-templates.md) and [Editing the MBAM 2.5 Group Policy Settings](editing-the-mbam-25-group-policy-settings.md) |  |
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | Deploy the MBAM client software. | [Deploying the MBAM 2.5 Client](deploying-the-mbam-25-client.md) |  |
