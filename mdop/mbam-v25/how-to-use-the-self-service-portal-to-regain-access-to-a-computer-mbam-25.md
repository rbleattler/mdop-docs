---
title: Use the Self-Service Portal to regain access to a computer
description: The Self-Service Portal is a website that IT administrators configure as part of their Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 deployment.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Use the Self-Service Portal to regain access to a computer

The Self-Service Portal is a website that IT administrators configure as part of their Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 deployment. The website enables users to independently regain access to their computers if they get locked out of Windows. The Self-Service Portal requires no assistance from Help Desk staff.

The following instructions are written from the perspective of users, but the information might be useful for IT administrators to understand.

> [!IMPORTANT]
> To be able to recover their key using the Self-Service Portal, a user must physically sign in to the computer (not remotely) at least one time successfully. Otherwise, they must use the Helpdesk Portal for key recovery.

Users might experience lockouts if they:

- Forget their password or PIN

- Change operating system files, the BIOS, or the Trusted Platform Module (TPM)

> [!NOTE]
> If the IT administrator configured an IIS Session State time-out, a message is displayed in the Self-Service Portal 60 seconds prior to the time-out.

## To use the Self-Service Portal to regain access to a computer

1.  In the **Recovery KeyId** field, enter a minimum of eight digits of the 32-digit BitLocker key ID that's displayed on the BitLocker recovery screen of your computer. If the first eight digits match multiple keys, a message displays that requires you to enter all 32 digits of the recovery key ID.

2.  In the **Reason** field, select a reason for your request for the recovery key.

3.  Select **Get Key**. Your BitLocker recovery key is displayed in the **Your BitLocker Recovery Key** field.

4.  To regain access to the computer, enter the 48-digit code into the BitLocker recovery screen on your computer.

## Related articles

[Performing BitLocker management with MBAM 2.5](performing-bitlocker-management-with-mbam-25.md)
