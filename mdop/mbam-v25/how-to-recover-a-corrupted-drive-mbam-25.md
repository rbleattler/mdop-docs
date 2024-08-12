---
title: Recover a corrupted drive
description: You can use this procedure with the Administration and Monitoring website (also referred to as the Help Desk) to recover a corrupted drive that's protected by BitLocker.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Recover a corrupted drive

You can use this procedure with the Administration and Monitoring website (also referred to as the Help Desk) to recover a corrupted drive that's protected by BitLocker. To do this, complete the following tasks:

- Create a recovery key package file by accessing the **Drive Recovery** area of the Administration and Monitoring website. To access the **Drive Recovery** area, you must be assigned the MBAM Helpdesk Users role or the MBAM Advanced Helpdesk Users role. You might have given these roles different names when you created them. For more information, see [Planning for MBAM 2.5 groups and accounts](planning-for-mbam-25-groups-and-accounts.md#bkmk-helpdesk-roles).

- Copy the package file to the computer that contains the corrupted drive.

- Use the `repair-bde` command to complete the recovery process. To avoid a potential loss of data, review the [`Manage-bde`](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff829849(v=ws.11)) command before using it.

## To recover a corrupted drive

1.  Open a web browser and navigate to the **Administration and Monitoring Website**.

2.  In the left pane, select **Drive Recovery** to open the **Recover access to an encrypted drive** page.

3.  Enter the end user's Windows sign-in domain and user name, the reason for unlocking the drive, and the end user's recovery password ID.

    > [!NOTE]
    > If you're a member of the Advanced Helpdesk Users access group, you don't have to enter the user's domain name or user name.

4.  Select **Submit**. The recovery key is displayed.

5.  Select **Save**, and then select **Recovery Key Package**. The recovery key package is created on your computer.

6.  Copy the recovery key package to the computer that has the corrupted drive.

7.  Open an elevated command prompt. To do this, select **Start** and type `cmd` in the **Search programs and files** text box. Right-click **cmd.exe**, and select **Run as Administrator**.

8.  At the command prompt, type the following command:

    `repair-bde <corrupted drive> <fixed drive> -kp <location of keypackage> -rp <recovery password>`

    > [!NOTE]
    > Replace &lt;*fixed drive*&gt; with an available hard disk drive that has free space equal to or larger than the data on the corrupted drive. Data on the corrupted drive is recovered and moved to the specified hard disk drive.

## Related articles

[Performing BitLocker management with MBAM 2.5](performing-bitlocker-management-with-mbam-25.md)
