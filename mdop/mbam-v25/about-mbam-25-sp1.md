---
title: About MBAM 2.5 SP1
description: Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 SP1 provides a simplified administrative interface for BitLocker Drive Encryption.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 09/27/2016
---

# About MBAM 2.5 SP1

Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 SP1 provides a simplified administrative interface for BitLocker Drive Encryption. BitLocker offers enhanced protection against data theft or data exposure for computers that are lost or stolen. BitLocker encrypts all data that is stored on the Windows operating system and drives and configured data drives.

## Overview of MBAM

MBAM 2.5 SP1 has the following features:

-   Enables administrators to automate the process of encrypting volumes on client computers across the enterprise.

-   Enables security officers to quickly determine the compliance state of individual computers or even of the enterprise itself.

-   Provides centralized reporting and hardware management with Microsoft System Center Configuration Manager.

-   Reduces the workload on the Help Desk to assist end users with BitLocker PIN and recovery key requests.

-   Enables end users to recover encrypted devices independently by using the Self-Service Portal.

-   Enables security officers to easily audit access to recover key information.

-   Empowers Windows Enterprise users to continue working anywhere with the assurance that their corporate data is protected.

MBAM enforces the BitLocker encryption policy options that you set for your enterprise, monitors the compliance of client computers with those policies, and reports on the encryption status of the enterprise's and individual's computers. In addition, MBAM lets you access the recovery key information when users forget their PIN or password, or when their BIOS or boot records change.

The following groups might be interested in using MBAM to manage BitLocker:

-   Administrators, IT security professionals, and compliance officers who are responsible for ensuring that confidential data isn't disclosed without authorization

-   Administrators who are responsible for computer security in remote or branch offices

-   Administrators who are responsible for client computers that are running Windows

> [!NOTE]
> BitLocker isn't explained in detail in this MBAM documentation. For more information, see [BitLocker Drive Encryption Overview](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732774(v=ws.11)).

## <a href="" id="what-s-new-in-mbam-2-5-sp1"></a>What's new in MBAM 2.5 SP1

This section describes the new features in MBAM 2.5 SP1.

### Newly supported languages for the MBAM 2.5 SP1 client

The following languages are now supported in MBAM 2.5 SP1 for the MBAM client only, including the Self-Service Portal:

- Czech (Czech Republic) cs-CZ

- Danish (Denmark) da-DK

- Dutch (Netherlands) nl-NL

- Finnish (Finland) fi-FI

- Greek (Greece) el-GR

- Hungarian (Hungary) hu-HU

- Norwegian, Bokmål (Norway) nb-NO

- Polish (Poland) pl-PL

- Portuguese (Portugal) pt-PT

- Slovak (Slovakia) sk-SK

- Slovenian (Slovenia) sl-SI

- Swedish (Sweden) sv-SE

- Turkish (Türkiye) tr-TR

For a list of all languages supported for client and server in MBAM 2.5 and MBAM 2.5 SP1, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).

### Support for Windows 10

MBAM 2.5 SP1 adds support for Windows 11, Windows 10, and Windows Server 2016, in addition to the same software that is supported in earlier versions of MBAM.

Windows 10 is supported in both MBAM 2.5 and MBAM 2.5 SP1.

### Support for Microsoft SQL Server 2014 SP1

MBAM 2.5 SP1 adds support for Microsoft SQL Server 2014 SP1, in addition to the same software that is supported in earlier versions of MBAM.

### MBAM no longer ships with separate MSI

Beginning in MBAM 2.5 SP1, a separate MSI is no longer included with the MBAM product. However, you can extract the MSI from the executable file (.exe) that is included with the product.

### MBAM can escrow OwnerAuth passwords without owning the TPM

Previously, if MBAM didn't own the TPM, the TPM OwnerAuth couldn't be escrowed to the MBAM database. To configure MBAM to own the TPM and to store the passwords, you had to disable TPM autoprovisioning and clear the TPM on the client computer.

In Windows 8 and higher, MBAM 2.5 SP1 can now escrow the OwnerAuth passwords without owning the TPM. During service startup, MBAM queries to see if the TPM is already owned and if so, it requests the passwords from the operating system. The passwords are then escrowed to the MBAM database. In addition, Group Policy must be set to prevent the OwnerAuth from being deleted locally.

In Windows 7, MBAM must own the TPM to automatically escrow TPM OwnerAuth information in the MBAM database. If MBAM doesn't own the TPM and Active Directory (AD) backup of the TPM is configured through Group Policy, you must use the **MBAM Active Directory (AD) Data Import cmdlets** to copy TPM OwnerAuth from AD into the MBAM database. These are five new PowerShell cmdlets that prepopulate MBAM databases with the Volume recovery and TPM owner information stored in Active Directory.

For more information, see [MBAM 2.5 security considerations](mbam-25-security-considerations.md#bkmk-tpm).

### MBAM can automatically unlock the TPM after a lockout

On computers running TPM 1.2, you can now configure MBAM to automatically unlock the TPM if it's locked out. If the TPM lockout auto reset feature is enabled, MBAM can detect that a user is locked out and then get the OwnerAuth password from the MBAM database to automatically unlock the TPM for the user.

This feature must be enabled on both the server side and in Group Policy on the client side. For more information, see [MBAM 2.5 security considerations](mbam-25-security-considerations.md#bkmk-autounlock).

### Support for FIPS-compliant BitLocker numerical password protectors

In MBAM 2.5, support was added for Federal Information Processing Standard (FIPS)-compliant BitLocker recovery keys on devices running the Windows 8.1 operating system. However, Windows didn't implement FIPS-compliant recovery keys in Windows 7. Therefore, Windows 7 and Windows 8 devices still required a Data Recovery Agent (DRA) protector for recovery.

The Windows team backported FIPS-compliant recovery keys with a hotfix, and MBAM 2.5 SP1 added support for them as well.

> [!NOTE]
> Client computers that are run Windows 8 still require a DRA protector since the hotfix wasn't backported to that OS. See [Hotfix Package 2 for BitLocker Administration and Monitoring 2.5](https://support.microsoft.com/topic/hotfix-package-2-for-bitlocker-administration-and-monitoring-2-5-8c51765a-99bb-d8ff-f55a-6182f5b674ae) to download and install the BitLocker hotfix for Windows 7 and Windows 8 computers. For information about DRA, see [Using data recovery agents with BitLocker](/previous-versions/windows/it-pro/windows-7/dd875560(v=ws.10)).

To enable FIPS compliance in your organization, you must configure the Federal Information Processing Standard (FIPS) Group Policy settings. For configuration instructions, see [BitLocker group policy settings](/windows/security/operating-system-security/data-protection/bitlocker/configure).

### Customize preboot recovery message and URL with new Group Policy setting

A new Group Policy setting, **Configure pre-boot recovery message and URL**, lets you configure a custom recovery message or specify a URL that is then displayed on the preboot BitLocker recovery screen when the OS drive is locked. This setting is only available on client computers running Windows 11 and Windows 10.

If you enable this policy setting, you can select one of these options for the preboot recovery message:

-   **Use custom recovery message**: Select this option to include a custom message in the preboot BitLocker recovery screen.

-   **Use custom recovery URL**: Select this option to replace the default URL that is displayed in the preboot BitLocker recovery screen.

-   **Use default recovery message and URL**: Select this option to display the default BitLocker recovery message and URL in the preboot BitLocker recovery screen. If you previously configured a custom recovery message or URL and want to revert to the default message, you must enable this policy and select this option.

The new Group Policy setting is located in the following GPO node: **Computer Configuration** &gt; **Policies** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **MDOP MBAM (BitLocker Management)** &gt; **Operating System Drive**. For more information, see [Planning for MBAM 2.5 group policy requirements](planning-for-mbam-25-group-policy-requirements.md).

### MBAM added support for Used Space Encryption

In MBAM 2.5 SP1, if you enable Used Space Encryption via BitLocker Group Policy, the MBAM Client honors it.

This Group Policy setting is called **Enforce drive encryption type on operating system drives** and is located in the following GPO node: **Computer Configuration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **BitLocker Drive Encryption** &gt; **Operating System Drives**. If you enable this policy and select the encryption type as **Used Space Only encryption**, MBAM honors the policy and BitLocker only encrypts disk space that's used on the volume.

For more information, see [Planning for MBAM 2.5 group policy requirements](planning-for-mbam-25-group-policy-requirements.md).

### MBAM Client support for Encrypted Hard Drives

MBAM supports BitLocker on Encrypted Hard Drives that meet TCG specification requirements for Opal and IEEE 1667 standards. When BitLocker is enabled on these devices, it generates keys and performs management functions on the encrypted drive. See [Encrypted Hard Drive](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831627(v=ws.11)) for more information.

### Delegation configuration no longer required when registering SPNs

The requirement to configure constrained delegation for SPNs that you register for the application pool account is no longer necessary in MBAM 2.5 SP1. However, it's still a requirement for MBAM 2.5.

### Enable BitLocker using MBAM as Part of a Windows Deployment

In MBAM 2.5 SP1, you can use a PowerShell script to configure BitLocker drive encryption and escrow recovery keys to the MBAM Server.

For more information, see [How to enable BitLocker by using MBAM as part of a Windows deployment](how-to-enable-bitlocker-by-using-mbam-as-part-of-a-windows-deploymentmbam-25.md).

### Self-Service Portal can be customized by using either PowerShell or the SSP customization wizard

As of MBAM 2.5 SP1, the Self-Service Portal can be configured by using the customization wizard and by using PowerShell. See [How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md).

### Web browser no longer unintentionally runs as administrator

An issue in MBAM 2.5 caused help links in the Server Configuration tool to cause browser windows to open with administrator rights. This issue is fixed in MBAM 2.5 SP1.

### No longer need to download the JavaScript files to configure the Self-Service Portal when the CDN is inaccessible

In MBAM 2.5 and earlier, the jQuery files used for configuration of the Self-Service Portal had to be downloaded from the CDN in advance if clients accessing the Self-Service Portal didn't have internet access. In MBAM 2.5 SP1, all JavaScript files are included in the product, so downloading them is unnecessary.

### Reports can be opened in Report Builder 3.0

In MBAM 2.5 SP1, the reports are updated to the latest report definition language schema, allowing users to open and customize the reports in Report Builder 3.0 and save them immediately without corrupting the report file.

### New PowerShell cmdlets

New PowerShell cmdlets for MBAM 2.5 SP1 enable you to configure and manage different MBAM features, including databases, reports, and web applications. Each feature has a corresponding PowerShell cmdlet that you can use to enable or disable features, or to get information about the feature.

The following cmdlets are implemented for MBAM 2.5 SP1:

-   Write-MbamTpmInformation

-   Write-MbamRecoveryInformation

-   Read-ADTpmInformation

-   Read-ADRecoveryInformation

-   Write-MbamComputerUser

The following parameters are implemented in the Enable-MbamWebApplication and Test-MbamWebApplication cmdlets for MBAM 2.5 SP1:

-   DataMigrationAccessGroup

-   TpmAutoUnlock

For information about the cmdlets, see [MBAM 2.5 security considerations](mbam-25-security-considerations.md) and [Microsoft BitLocker Administration and Monitoring cmdlet help](/powershell/mdop/get-started).

### MBAM agent detects presentation mode

The MBAM agent can detect when the computer is in presentation mode and avoid invoking the MBAM UI at that time.

### MBAM agent service now configured to use delayed start

After installation, the service will now set the MBAM agent service to use delayed start, decreasing the amount of time it takes to start Windows.

### Locked Fixed Data volumes now report as Compliant

The compliance calculation logic for "Locked Fixed Data" volumes changed to report the volumes as "Compliant," but with a Protector State and Encryption State of "Unknown" and with a Compliance Status Detail of "Volume is locked". Previously, locked volumes were reported as "Non-Compliant", a Protector State of "Encrypted", an Encryption State of "Unknown", and a Compliance Status Detail of "An unknown error".

## MBAM 2.5 SP1 Release Notes

For more information and late-breaking news that isn't included in this documentation, see [Release Notes for MBAM 2.5 SP1](release-notes-for-mbam-25-sp1.md).
