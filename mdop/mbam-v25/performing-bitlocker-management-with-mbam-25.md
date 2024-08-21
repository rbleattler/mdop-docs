---
title: Perform BitLocker management with MBAM 2.5
description: The information in this article describes post-installation, day-to-day BitLocker encryption management tasks that are accomplished by using Microsoft BitLocker Administration and Monitoring.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Perform BitLocker management with MBAM 2.5

After you plan for and then deploy Microsoft BitLocker Administration and Monitoring (MBAM), you can configure and use it to manage BitLocker Drive Encryption across your organization. The information in this article describes post-installation, day-to-day BitLocker encryption management tasks that are accomplished by using Microsoft BitLocker Administration and Monitoring.

## Reset a TPM lockout

A Trusted Platform Module (TPM) is a microchip that is designed to provide basic security-related functions, primarily involving encryption keys. The TPM is installed on the motherboard of a computer, and it communicates with the rest of the system by using a host bus adapter. On computers that incorporate a TPM, you can create cryptographic keys and encrypt them so that only the TPM can decrypted them.

A TPM lockout can occur if a user enters the incorrect PIN too many times. The number of times that a user can enter an incorrect PIN before the TPM locks varies by manufacturer. You can use MBAM to access the centralized key recovery data system on the Administration and Monitoring website, where you can retrieve a TPM owner password file when you supply a computer ID and an associated user identifier.

[How to reset a TPM lockout](how-to-reset-a-tpm-lockout-mbam-25.md)

## Recover drives

When you deal with the encryption of data, especially in a large organization, consider how that data can be recovered. For example, a hardware failure, changes in personnel, or other situations in which encryption keys can be lost.

The encrypted drive recovery features in MBAM ensure that data can be captured and stored and that the required tools are available to access a BitLocker-protected volume when BitLocker goes into recovery mode, is moved, or becomes corrupted.

[How to recover a drive in recovery mode](how-to-recover-a-drive-in-recovery-mode-mbam-25.md)

[How to recover a moved drive](how-to-recover-a-moved-drive-mbam-25.md)

[How to recover a corrupted drive](how-to-recover-a-corrupted-drive-mbam-25.md)

## Determine BitLocker encryption state of lost computers

By using MBAM, you can determine the last known BitLocker encryption status of computers that were lost or stolen.

[How to determine BitLocker encryption state of lost computers](how-to-determine-bitlocker-encryption-state-of-lost-computers-mbam-25.md)

## Use the Self-Service Portal to regain access to a computer

If end users get locked out of Windows by BitLocker, they can use the instructions in this section to get a BitLocker recovery key to regain access to their computer.

[How to use the Self-Service Portal to regain access to a computer](how-to-use-the-self-service-portal-to-regain-access-to-a-computer-mbam-25.md)

## Related articles

[Operations for MBAM 2.5](operations-for-mbam-25.md)
