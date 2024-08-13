---
title: Client event logs
description: This article contains event IDs that can occur on the MBAM client.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.topic: reference
ms.date: 06/16/2016
---

# Client Event Logs

MBAM client event logs are located in Event Viewer - Applications and Services Logs - Microsoft - Windows - MBAM - Operational path.
The following table contains event IDs that can occur on the MBAM client.

| Event ID | Channel | Event symbol | Message |
|--|--|--|--|
| 1 | Operational | VolumeEnactmentSuccessful | The MBAM policies were applied successfully. |
| 2 | Admin | VolumeEnactmentFailed | An error occurred while applying MBAM policies. |
| 3 | Operational | TransferStatusDataSuccessful | The encryption status data was sent successfully. |
| 4 | Admin | TransferStatusDataFailed | An error occurred while sending encryption status data. |
| 8 | Admin | SystemVolumeNotFound | The system volume is missing. SystemVolume is needed to encrypt the operating system drive. |
| 9 | Admin | TPMNotFound | The TPM hardware is missing. TPM is needed to encrypt the operating system drive with any TPM protector. |
| 10 | Admin | MachineHWExempted | The computer is exempted from Encryption. Machine's hardware status: Exempted |
| 11 | Admin | MachineHWUnknown | The computer is exempted from encryption. Machine's hardware status: Unknown |
| 12 | Admin | HWCheckFailed | Hardware exemption check failed. |
| 13 | Admin | UserIsExempted | The user is exempt from encryption. |
| 14 | Admin | UserIsWaiting | The user requested an exemption. |
| 15 | Admin | UserExemptionCheckFailed | User exemption check failed. |
| 16 | Admin | UserPostponed | The user postponed the encryption process. |
| 17 | Admin | TPMInitializationFailed | TPM initialization failed. The user rejected the BIOS changes. |
| 18 | Admin | CoreServiceDown | Unable to connect to the MBAM Recovery and Hardware service. |
| 19 | Operational | CoreServiceUp | Successfully connected to the MBAM Recovery and Hardware service. |
| 20 | Admin | PolicyMismatch | The MBAM policy is in conflict or corrupt. |
| 21 | Admin | ConflictingOSVolumePolicies | Detected OS volume encryption policies conflict. Check BitLocker and MBAM policies related to OS drive protectors. |
| 22 | Admin | ConflictingFDDVolumePolicies | Detected Fixed Data Drive volume encryption policies conflict. Check BitLocker and MBAM policies related to FDD drive protectors. |
| 27 | Admin | EncryptionFailedNoDra | An error occurred while encrypting. A Data Recovery Agent (DRA) protector is required in FIPS mode for pre-Windows 8.1 machines. |
| 28 | Operational | TpmOwnerAuthEscrowed | The TPM OwnerAuth has been escrowed. |
| 29 | Operational | RecoveryKeyEscrowed | The BitLocker recovery key for the volume has been escrowed. |
| 30 | Operational | RecoveryKeyReset | The BitLocker recovery key for the volume has been updated. |
| 31 | Operational | EnforcePolicyDateSet | The enforce policy date, <em>&lt;date&gt;</em>, has been set for the volume |
| 32 | Operational | EnforcePolicyDateCleared | The enforce policy date, <em>&lt;date&gt;</em>, has been cleared for the volume. |
| 33 | Operational | TpmLockOutResetSucceeded | Successfully reset TPM lockout. |
| 34 | Admin | TpmLockOutResetFailed | Failed to reset TPM lockout. |
| 35 | Operational | TpmOwnerAuthRetrievalSucceeded | Successfully retrieved TPM OwnerAuth from MBAM services. |
| 36 | Admin | TpmOwnerAuthRetrievalFailed | Failed to retrieve TPM OwnerAuth from MBAM services. |
| 37 | Admin | WmiProviderDllSearchPathUpdateFailed | Failed to update the DLL search path for WMI provider. |
| 38 | Admin | TimedOutWaitingForWmiProvider | Agent Stopping - Timed-out waiting for MBAM WMI Provider Instance. |
| 39 | Operational | RemovableDriveMounted | Removable drive was mounted. |
| 40 | Operational | RemovableDriveDismounted | Removable drive was unmounted. |
| 41 | Operational | FailedToEnactEndpointUnreachable | Failure to connect to the MBAM Recovery and Hardware service prevented MBAM policies from being applied successfully to the volume. |
| 42 | Operational | FailedToEnactLockedVolume | Locked volume state prevented MBAM policies from being applied successfully to the volume. |
| 43 | Operational | TransferStatusDataFailedEndpointUnreachable | Failure to connect to the MBAM Compliance and Status service prevented the transfer of encryption status data. |

## Related articles

[Server event logs](server-event-logs.md)
