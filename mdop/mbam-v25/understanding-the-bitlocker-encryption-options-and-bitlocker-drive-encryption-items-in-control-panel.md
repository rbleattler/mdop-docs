---
title: Understanding the BitLocker encryption options and BitLocker Drive Encryption items in Control Panel
description: This article describes the BitLocker encryption options and BitLocker Drive Encryption Control Panel items.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Understanding the BitLocker encryption options and BitLocker Drive Encryption items in Control Panel

This article describes the **BitLocker Encryption Options** and **BitLocker Drive Encryption** Control Panel items. It explains how these items are created and the tasks they enable you to do.

- **Manage BitLocker** "right-click" shortcut menu, when it's visible versus hidden, and how to set it to be visible by default.

## BitLocker encryption options and BitLocker Drive Encryption Control Panel items

The following table lists the tasks you can do from each Control Panel item and describes how these items are created.

| Description | BitLocker encryption options (MBAM) | BitLocker Drive Encryption (Windows) |
|--|--|--|
| **Tasks you can do** | - Change your PIN or password <br> - Check encryption status for a drive <br> - Open the TPM Management console <br> - Turn on BitLocker | - Suspend protection for a drive <br> - Back up your recovery key <br> - Change your PIN <br> - Turn off BitLocker for a drive <br> - Turn on BitLocker for a drive <br> - Open the TPM Management console <br> - Decrypt a drive (appears only if the MBAM client is NOT installed) |
| **How the Control Panel item is created** | Created in Control Panel when you install the MBAM client. This item can't be hidden. <br> **Note:** This item appears in addition to, but doesn't replace, the default BitLocker Drive Encryption Control Panel item. | Appears by default in Control Panel as part of the Windows operating system, but you can hide it. <br> To hide it, see [Hiding the default BitLocker Drive Encryption item in Control Panel](hiding-the-default-bitlocker-drive-encryption-item-in-control-panel-mbam-25.md). |

## <a href="" id="-manage-bitlocker--shortcut-menu"></a>"Manage BitLocker" shortcut menu

The following table describes how the **Manage BitLocker** shortcut menu differs depending on whether the MBAM client is installed. The term "shortcut menu" refers to options that appear when you right-click a drive in Windows Explorer.

| Description | When MBAM client is installed | When MBAM client isn't installed |
|--|--|--|
| Visibility of shortcut menu | The Manage BitLocker option is hidden. <br> To make the Manage BitLocker option visible on the shortcut menu, which displays the option to decrypt a drive, delete the following registry key: <br> `HKEY_CLASSES_ROOT\Drive\Shell\manage-bde \REG_SZ LegacyDisable` | The Manage BitLocker option appears on the shortcut menu. |
| What users can do | With the shortcut hidden, users can open the BitLocker Drive Encryption Control Panel item, but the option to decrypt a drive isn't available. | With the shortcut visible, selecting the **Manage BitLocker** option opens the BitLocker Drive Encryption Control Panel item, which displays the option to decrypt a drive. |

## Related articles

[Administering MBAM 2.5 features](administering-mbam-25-features.md)
