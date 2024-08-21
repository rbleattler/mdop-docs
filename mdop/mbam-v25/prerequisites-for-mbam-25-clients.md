---
title: Prerequisites for MBAM 2.5 clients
description: Before you install the Microsoft BitLocker Administration and Monitoring (MBAM) client software on computers, ensure that your environment and the client computers meet the following prerequisites.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/23/2017
---

# Prerequisites for MBAM 2.5 clients

Before you install the Microsoft BitLocker Administration and Monitoring (MBAM) client software on computers, ensure that your environment and the client computers meet the following prerequisites.

| Prerequisite | Details |
|--|--|
| The enterprise domain must contain at least one Windows Server 2008 (or later) domain controller. |  |
| The client computer must be logged on to the enterprise intranet. |  |
| For Windows 7 client computers only: Each client must have Trusted Platform Module (TPM) capability (TPM 1.2 or later). |  |
| For Windows 8.1, Windows 10 RTM, or Windows 10 version 1511 client computers only: If you want MBAM to be able to store and manage the TPM recovery keys, TPM autoprovisioning must be turned off, and MBAM must be set as the owner of the TPM before you deploy MBAM. <br> In MBAM 2.5 SP1 only, you no longer need to turn off TPM autoprovisioning, but you must make sure that the TPM group policy objects are set to not escrow TPM OwnerAuth to Active Directory. | [MBAM 2.5 security considerations](mbam-25-security-considerations.md#bkmk-tpm) |
| For Windows 10, version 1607 or later, only Windows can take ownership of the TPM. In addition, Windows won't retain the TPM owner password when provisioning the TPM. <br> In MBAM 2.5 SP1, you must turn on autoprovisioning. | For more information, see [TPM owner password](/windows/security/hardware-security/tpm/change-the-tpm-owner-password). |
| The TPM chip must be turned on in the BIOS and be resettable from the operating system. | For more information, see the BIOS documentation. |
| The computer's hard disk must have at least two partitions and must be formatted with the NTFS file system. |  |
| The computer's hard disk must have a BIOS that is compatible with TPM and that supports USB devices during computer startup. <br> **Note:** Ensure that the keyboard, video, or mouse are directly connected and not managed through a keyboard, video, or mouse (KVM) switch. A KVM switch can interfere with the ability of the computer to detect the physical presence of hardware. |  |
| If you use a proxy, it must be visible in the system context. MBAM runs under the system context, not the user context. |  |

> [!IMPORTANT]
> If BitLocker was used without MBAM, MBAM can be installed and utilize the existing TPM information.

## Related articles

[MBAM 2.5 supported configurations](mbam-25-supported-configurations.md)

[Planning to deploy MBAM 2.5](planning-to-deploy-mbam-25.md)
