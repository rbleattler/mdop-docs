---
title: Recover a drive in recovery mode
description: This article explains how to use the Administration and Monitoring website (also referred to as the Help Desk) to get a recovery password to give to end users if their BitLocker-protected drive goes into recovery mode.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Recover a drive in recovery mode

This article explains how to use the Administration and Monitoring website (also referred to as the Help Desk) to get a recovery password to give to end users if their BitLocker-protected drive goes into recovery mode. Drives go into recovery mode if users lose or forget their PIN or password or if the Trusted Module Platform (TPM) chip detects changes to the BIOS or startup files of a computer.

To get a recovery password, use the **Drive Recovery** area of the Administration and Monitoring Website. You must be assigned the MBAM Helpdesk Users role or the MBAM Advanced Helpdesk Users role to access this area of the website.

> [!NOTE]
> You may have given these roles different names when you created them. For more information, see [Planning for MBAM 2.5 groups and accounts](planning-for-mbam-25-groups-and-accounts.md#bkmk-helpdesk-roles).

> [!IMPORTANT]
> Recovery passwords expire after a single use. On OS drives and fixed data drives, the single-use rule is applied automatically. On removable drives, it's applied when the drive is removed and then reinserted and unlocked on a computer that has group policy settings activated to manage removable drives.

## To recover a drive in recovery mode

1.  Open a web browser and navigate to the **Administration and Monitoring Website**.

2.  In the left pane, select **Drive Recovery** to open the **Recover access to an encrypted drive** page.

3.  Enter the user's Windows sign-in domain and user name to view recovery information.

    > [!NOTE]
    > If you're in the MBAM Advanced Helpdesk Users group, the user domain and user ID fields aren't required.

4.  Enter the first eight digits of the recovery key ID to see a list of possible matching recovery keys, or enter the entire recovery key ID to get the exact recovery key.

5.  From the **Reason for Drive Unlock** list, select one of the predefined options, and then select **Submit**.

    MBAM returns the following information:

    - An error message if no matching recovery password is found.

    - Multiple possible matches if the user has multiple matching recovery passwords.

    - The recovery password and recovery package for the submitted user.

        > [!NOTE]
        > If you're recovering a damaged drive, the recovery package option provides BitLocker with critical information that it needs to recover the drive.

    After the recovery password and recovery package are retrieved, the recovery password is displayed.

6. To copy the password, select **Copy Key**, and then paste the recovery password into an email message. Alternatively, select **Save** to save the recovery password to a file.

   When the user types the recovery password into the system or uses the recovery package, the drive is unlocked.

## Related articles

[Performing BitLocker management with MBAM 2.5](performing-bitlocker-management-with-mbam-25.md)
