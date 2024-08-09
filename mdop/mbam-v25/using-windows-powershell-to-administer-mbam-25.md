---
title: Using Windows PowerShell to administer MBAM 2.5
description: This article describes Windows PowerShell cmdlets for Microsoft BitLocker Administration and Monitoring (MBAM) that relate to recovering computers or drives when users get locked out.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 11/02/2016
---

# Using Windows PowerShell to administer MBAM 2.5

This article describes Windows PowerShell cmdlets for Microsoft BitLocker Administration and Monitoring (MBAM) that relate to recovering computers or drives when users get locked out.

For cmdlets that you use to configure MBAM Server features, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md).

## <a href="" id="cmdlets-for-recovering-computers-or-drives-that-are-managed-by-mbam-"></a>Cmdlets for recovering computers or drives that MBAM manages

Use the following Windows PowerShell cmdlets to recover computers or drives that MBAM manages.

| Name | Description |
|--|--|
| Get-MbamBitLockerRecoveryKey | Requests an MBAM recovery key that enables users to unlock a computer or encrypted drive. |
| Get-MbamTPMOwnerPassword | Provides users with a TPM owner password that they can use to unlock a Trusted Platform Module (TPM) when the TPM locks them out and doesn't accept their PIN. |

## <a href="" id="---------mbam-cmdlet-help"></a> MBAM cmdlet help

Windows PowerShell Help for MBAM cmdlets is available in the following formats:

- At a Windows PowerShell command prompt, type `Get-Help <cmdlet>`

  To get the latest Windows PowerShell cmdlets, follow the instructions in [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md).

- [MDOP PowerShell modules](/powershell/mdop/get-started)

- [Cmdlet reference download for MDOP](https://www.microsoft.com/download/details.aspx?id=41195)

## Related articles

[Administering MBAM 2.5 features](administering-mbam-25-features.md)

[Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md)
