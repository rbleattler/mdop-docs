---
title: Deploying MBAM 2.5 group policy objects
description: To deploy Microsoft BitLocker Administration and Monitoring (MBAM), you have to set group policy settings that define MBAM implementation settings for BitLocker drive encryption.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Deploying MBAM 2.5 group policy objects

To deploy Microsoft BitLocker Administration and Monitoring (MBAM), you have to set group policy settings that define MBAM implementation settings for BitLocker drive encryption. To complete this task, you must copy the MBAM group policy templates to a server or workstation that are capable of running Group Policy Management Console (GPMC) or Advanced Group Policy Management (AGPM), and then edit the settings.

> [!IMPORTANT]
> Don't change the group policy settings in the **BitLocker Drive Encryption** node, or MBAM will not work correctly. When you configure the group policy settings in the **MDOP MBAM (BitLocker Management)** node, MBAM automatically configures the **BitLocker Drive Encryption** settings for you.

## Copying the MBAM 2.5 group policy templates

Before you install the MBAM Client, you must copy MBAM-specific group policy objects (GPOs) to the Management Workstation. These GPOs define MBAM implementation settings for BitLocker drive encryption. You can copy the group policy templates to any server or workstation that is a supported Windows server or client computer and that is able to run the Group Policy Management Console (GPMC) or Advanced Group Policy Management (AGPM).

[Copying the MBAM 2.5 group policy templates](copying-the-mbam-25-group-policy-templates.md)

## Editing MBAM 2.0 GPO settings

After you create the necessary GPOs, you must deploy the MBAM group policy settings to your organization's client computers. To view and create GPOs, you must have Group Policy Management Console (GPMC) or Advanced Group Policy Management (AGPM) installed.

[Editing the MBAM 2.5 group policy settings](editing-the-mbam-25-group-policy-settings.md)

## Showing or hiding the MBAM Control Panel in Windows Control Panel

Since MBAM offers a customized MBAM control panel that can replace the default Windows BitLocker control panel, you can also choose to show or hide the default BitLocker Control Panel from end users by using group policy settings.

[Hiding the default BitLocker Drive Encryption item in Control Panel](hiding-the-default-bitlocker-drive-encryption-item-in-control-panel-mbam-25.md)
