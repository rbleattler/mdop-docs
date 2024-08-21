---
title: Determining why a device receives a noncompliance message
description: The following noncompliance codes are provided by WMI and describe the reasons why MBAM reports a particular device as noncompliant.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/22/2017
---

# Determining why a device receives a noncompliance message

The following noncompliance codes are provided by WMI and describe the reasons why MBAM reports a particular device as noncompliant.

You can use your preferred method to view WMI. If you use Windows PowerShell, run `gwmi -class mbam_volume -Namespace root\microsoft\mbam` from a PowerShell prompt and search for `ReasonsForNoncompliance`.

| Noncompliance code | Reason for noncompliance |
|--|--|
| 0 | Cipher strength not AES 256. |
| 1 | MBAM policy requires this volume to be encrypted but it isn't. |
| 2 | MBAM policy requires this volume to NOT be encrypted, but it is. |
| 3 | MBAM policy requires this volume use a TPM protector, but it doesn't. |
| 4 | MBAM policy requires this volume use a TPM+PIN protector, but it doesn't. |
| 5 | MBAM policy doesn't allow non TPM machines to report as compliant. |
| 6 | Volume has a TPM protector but the TPM isn't visible (booted with recover key after disabling TPM in BIOS?). |
| 7 | MBAM policy requires this volume use a password protector, but it doesn't have one. |
| 8 | MBAM policy requires this volume NOT use a password protector, but it has one. |
| 9 | MBAM policy requires this volume use an autounlock protector, but it doesn't have one. |
| 10 | MBAM policy requires this volume NOT use an autounlock protector, but it has one. |
| 11 | Policy conflict detected preventing MBAM from reporting this volume as compliant. |
| 12 | A system volume is needed to encrypt the OS volume but it isn't present. |
| 13 | Protection is suspended for the volume. |
| 14 | Auto-Unlock unsafe unless the OS volume is encrypted. |
| 15 | Policy requires minimum cypher strength is XTS-AES-128 bit. Actual cypher strength is weaker than that. |
| 16 | Policy requires minimum cypher strength is XTS-AES-256 bit. Actual cypher strength is weaker than that. |

## Related articles

[Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md)
