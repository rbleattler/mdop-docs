---
title: Reset a TPM lockout
description: This article explains how to use the Administration and Monitoring website (also referred to as the Help Desk) to reset a TPM lockout.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Reset a TPM lockout

This article explains how to use the Administration and Monitoring website (also referred to as the Help Desk) to reset a TPM lockout. TPM lockouts can occur if an end user enters the incorrect PIN too many times. The number of times that a user can enter an incorrect PIN before the TPM locks varies from manufacturer to manufacturer.

From the **Manage TPM** area of the Administration and Monitoring website, you can access the centralized Key Recovery data system, which provides a TPM owner password file when you supply a computer ID and associated user identifier.

To access the Manage TPM area of the Administration and Monitoring website, you must be assigned the MBAM Helpdesk Users role or the MBAM Advanced Helpdesk Users role. These roles are groups that administrators create in Active Directory. You can use any name for these groups. For more information, see [Planning for MBAM 2.5 groups and accounts](planning-for-mbam-25-groups-and-accounts.md#bkmk-helpdesk-roles).

For information about MBAM and TPM ownership, see [MBAM 2.5 security considerations](mbam-25-security-considerations.md#bkmk-tpm).

## To reset a TPM lockout

1.  Open a web browser and navigate to the **Administration and Monitoring Website**.

2.  In the left pane, select **Manage TPM** to open the **Manage TPM** page.

3.  Enter the fully qualified domain name for the computer and the computer name.

4.  Enter the end user's Windows sign-in domain and user name to retrieve the TPM owner password file.

    > [!NOTE]
    > If you're in the MBAM Advanced Helpdesk Users group, the user domain and user ID fields aren't required.

5.  From the **Reason for requesting TPM owner password file** list, select a reason for the request, and select **Submit**.

    MBAM returns one of the following information:

    - An error message if no matching TPM owner password file is found

    - The TPM owner password file for the submitted computer

    After the TPM owner password is retrieved, the owner password is displayed.

6.  To save the password to a `.tpm` file, select the **Save** button.

7.  In the **Manage TPM** area of the **Administration and Monitoring Website**, select the **Reset TPM lockout** option and provide the TPM owner password file.

    The TPM lockout is reset and the user's access is restored.

    > [!IMPORTANT]
    > Don't give the TPM hash value or TPM owner password file to users. Because the TPM information doesn't change, giving the file to users creates a security risk.

## Related articles

[Performing BitLocker management with MBAM 2.5](performing-bitlocker-management-with-mbam-25.md)
