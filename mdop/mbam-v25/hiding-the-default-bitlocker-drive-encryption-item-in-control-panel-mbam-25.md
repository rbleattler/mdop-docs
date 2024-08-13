---
title: Hiding the default BitLocker Drive Encryption item in Control Panel
description: This article describes how to hide the **BitLocker Drive Encryption** Control Panel item, which appears by default on Control Panel as part of the Windows operating system.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Hiding the default BitLocker Drive Encryption item in Control Panel

This article describes how to hide the **BitLocker Drive Encryption** Control Panel item, which appears by default on Control Panel as part of the Windows operating system.

> [!NOTE]
> Microsoft BitLocker Administration and Monitoring (MBAM) creates an additional, custom Control Panel item, called **BitLocker Encryption Options**. It enables users to manage their PIN and password, turn on BitLocker for a drive, and check encryption.

For more information about the following topics, see [Understanding the BitLocker encryption options and BitLocker Drive Encryption items in Control Panel](understanding-the-bitlocker-encryption-options-and-bitlocker-drive-encryption-items-in-control-panel.md):

- Differences between the MBAM and the default Control Panel items.

- **Manage BitLocker** shortcut menu that appears when you right-click a drive in Windows Explorer.

> [!IMPORTANT]
> Don't change the group policy settings in the **BitLocker Drive Encryption** node. If you do, MBAM doesn't work correctly. When you configure the group policy settings in the **MDOP MBAM (BitLocker Management)** node, MBAM automatically configures the **BitLocker Drive Encryption** settings for you.

## To hide the default BitLocker Drive Encryption item in Control Panel

1.  In the Group Policy Management Console (GPMC) or in Advanced Group Policy Management, browse to **User configuration** &gt; **Policies** &gt; **Administrative Templates** &gt; **Control Panel**.

2.  In the **Details** pane, double-click **Hide specified Control Panel items**, and then select **Enabled**.

3.  Select **Show**, select **Add**, and then type **Microsoft.BitLockerDriveEncryption**.

## Related articles

[Understanding the BitLocker encryption options and BitLocker Drive Encryption items in Control Panel](understanding-the-bitlocker-encryption-options-and-bitlocker-drive-encryption-items-in-control-panel.md)

[Deploying MBAM 2.5 group policy objects](deploying-mbam-25-group-policy-objects.md)
