---
title: Recover a moved drive
description: This article explains how to use the Administration and Monitoring Website (also referred to as the Help Desk) to recover an OS drive that was moved after being encrypted by Microsoft BitLocker Administration and Monitoring (MBAM).
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 11/01/2016
---

# Recover a moved drive

This article explains how to use the Administration and Monitoring Website (also referred to as the Help Desk) to recover an OS drive that was moved after being encrypted by Microsoft BitLocker Administration and Monitoring (MBAM). When a drive is moved, it no longer accepts the PIN that was used in the previous computer because the Trusted Platform Module (TPM) chip changed. To recover the moved drive, you must obtain the recovery key ID to retrieve the recovery password.

To recover a moved drive, you must use the **Drive Recovery** area of the Administration and Monitoring Website. To access the **Drive Recovery** area, you must be assigned the MBAM Helpdesk Users role or the MBAM Advanced Helpdesk Users role. For more information about these roles, see [Planning for MBAM 2.5 groups and accounts](planning-for-mbam-25-groups-and-accounts.md#bkmk-helpdesk-roles).

## To recover a moved drive

1.  On the computer that contains the moved drive, start the computer in Windows Recovery Environment (WinRE) mode, or start the computer by using the Microsoft Diagnostic and Recovery Toolset (DaRT).

2.  After the computer starts with WinRE or DaRT, MBAM treats the moved OS drive as a fixed data drive. MBAM then displays the drive's recovery password ID and asks for the recovery password.

    > [!NOTE]
    > In some cases, you can click **I forgot the PIN** during the startup process, and then enter the recovery mode to display the recovery key ID.

3.  Use the recovery key ID to retrieve the recovery password and unlock the drive from the Administration and Monitoring Website. For more information, see [How to recover a drive in recovery mode](how-to-recover-a-drive-in-recovery-mode-mbam-25.md).

    If the moved drive was configured to use a TPM chip on the original computer, complete the following steps. Otherwise, the recovery process is complete.

4.  After unlocking the drive and completing the start process, open a command prompt in WinRE mode and use the `manage-bde` command to decrypt the drive. Using this tool is the only way to remove the TPM plus the PIN protector without the original TPM chip. For information about the `manage-bde` command, see [`Manage-bde`](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff829849(v=ws.11)).

5.  When the removal is completed, start the computer normally. The MBAM agent will now enforce the policy to encrypt the drive with the new computer's TPM plus the PIN.

## Related articles

[Performing BitLocker management with MBAM 2.5](performing-bitlocker-management-with-mbam-25.md)
