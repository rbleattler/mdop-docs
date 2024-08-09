---
title: Understanding MBAM 2.5 stand-alone reports
description: This article describes the reports that are available when you use Microsoft BitLocker Administration and Monitoring (MBAM) in the stand-alone topology.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Understanding MBAM 2.5 stand-alone reports

This article describes the reports that are available when you use Microsoft BitLocker Administration and Monitoring (MBAM) in the stand-alone topology.

> [!NOTE]
> If you use MBAM with the Configuration Manager integration topology, you generate reports from Configuration Manager rather than from MBAM. For more information about these reports, see [Viewing MBAM 2.5 reports for the Configuration Manager integration topology](viewing-mbam-25-reports-for-the-configuration-manager-integration-topology.md).

## Understanding the MBAM stand-alone topology reports

MBAM provides three report types that you can use to monitor your organization for BitLocker compliance:

- [Enterprise Compliance Report](#bkmk-enterprisecompliance)

- [Computer Compliance Report](#bkmk-compliance)

- [Recovery Audit Report](#bkmk-recovery)

To access MBAM reports when you use MBAM in the stand-alone topology, open a web browser, and then open the Administration and Monitoring website. Select **Reports** in the left menu bar. From the top menu bar, select the kind of report that you want to generate. For more information about generating these reports, see [Generating MBAM 2.5 stand-alone reports](generating-mbam-25-stand-alone-reports.md).

### <a href="" id="bkmk-enterprisecompliance"></a>Enterprise compliance report

Use this report type to collect information about overall BitLocker compliance in your organization. You can use filters to narrow your search results to learn more about the compliance state and error status of computers in your organization.

#### Enterprise compliance overview

| Column Name | Description |
|--|--|
| Managed Computers | Number of computers that MBAM manages. |
| % Compliant | Percentage of compliant computers in the enterprise. |
| % Non-Compliant | Percentage of noncompliant computers in the enterprise. |
| % Exempt | Percentage of computers exempt from the BitLocker encryption requirement. |
| % Non-Exempt | Percentage of computers not exempt from the BitLocker encryption requirement. |
| Compliant | Percentage of compliant computers in the enterprise. |
| Non-Compliant | Percentage of noncompliant computers in the enterprise. |
| Exempt | Total computers that are exempt from the BitLocker encryption requirement. |
| Non-Exempt | Total computers that aren't exempt from the BitLocker encryption requirement. |

#### Enterprise compliance computer details

|| Column Name | Description |
|--|--|
| Computer Name | User-specified DNS name that MBAM manages. |
| Domain Name | Fully qualified domain name where the client computer resides and MBAM manages. |
| Compliance Status | State of compliance for the computer, according to the policy specified for the computer. The states are Noncompliant and Compliant. For more information about how to interpret compliance states, see the following Enterprise Compliance Report Compliance States table. |
| Exemption | Status that indicates whether this computer is exempt from the BitLocker policy. |
| Compliance Status Details | Error and status messages about the compliance state of the computer in accordance with the policy specified. |
| Last Contact | Date and time when the computer last contacted the server to report compliance status. The contact frequency is configurable. For more information, see the MBAM Group Policy settings. |

### <a href="" id="bkmk-compliance"></a>Computer compliance report

Use this report type to collect information that is specific to a computer or user.

View this report by clicking the computer name in the Enterprise Compliance Report, or by typing the computer name in the Computer Compliance Report. This report shows detailed encryption information about each drive (operating system and fixed data drives) on a computer. It also indicates the policy that is applied to each drive type on the computer. To view the details of each drive, expand the Computer Name entry.

> [!NOTE]
> Removable Data Volume encryption status isn't shown in this report.

#### Computer compliance report fields

| Column Name | Description |
|--|--|
| Computer Name | User-specified DNS computer name that MBAM manages. |
| Domain Name | Fully qualified domain name where the client computer resides and MBAM manages. |
| Computer Type | Type of computer. Valid types are Non-Portable and Portable. |
| Operating System | Operating system type found on the client computer that MBAM manages. |
| Compliance Status | Overall compliance status of the computer that MBAM manages. Valid states are Compliant and Noncompliant. |
| Policy Cipher Strength | Cipher strength selected by the administrator during MBAM policy specification (for example, 128-bit with diffuser). |
| Policy Operating System Drive | Indicates if encryption is required for the operating system and shows the appropriate protector type. |
| Policy-Fixed Data Drive | Indicates if encryption is required for the fixed data drive. |
| Policy Removable Data Drive | Indicates if encryption is required for the removable drive. |
| Device Users | Known users on the computer that MBAM manages. |
| Exemption | Status that indicates whether this computer is exempt from the BitLocker policy. |
| Manufacturer | Computer manufacturer name, as it appears in the computer BIOS. |
| Model | Computer manufacturer model name, as it appears in the computer BIOS. |
| Compliance Status Details | Error and status messages about the compliance state of the computer, in accordance with the specified policy. |
| Last Contact | Date and time that the computer last contacted the server to report compliance status. The contact frequency is configurable. For more information, see the MBAM Group Policy settings. |

#### Computer compliance report drive fields

| Column Name | Description |
|--|--|
| Drive Letter | Computer drive letter that the user assigned to the particular drive. |
| Drive Type | Type of drive. Valid values are Operating System Drive and Fixed Data Drive. These are physical drives rather than logical volumes. |
| Cipher Strength | Cipher strength selected by the administrator during MBAM policy specification. |
| Protector Type | Type of protector selected through the Group Policy setting used to encrypt an operating system or fixed data volume. |
| Protector State | Indicates that the computer that MBAM manages enabled the protector type that the policy specifies. The valid states are ON or OFF. |
| Encryption State | Encryption state of the drive. Valid states are Encrypted, Not Encrypted, and Encrypting. |
| Compliance Status | State that indicates whether the drive is in accordance with the policy. States are Noncompliant and Compliant. |
| Compliance Status Details | Error and status messages of the compliance state of the computer, according to the specified policy. |

### <a href="" id="bkmk-recovery"></a>Recovery audit report

Use this report type to audit users who requested access to BitLocker recovery keys. The report offers several filters based on the desired filtering criteria. You can filter on a specific type of user (a Help Desk user or an end user), whether the request failed or was successful, the specific type of key requested, and a date range during which the retrieval occurred.

#### Recovery audit report fields

| Column Name | Description |
|--|--|
| Request Date and Time | Date and time that a key retrieval request was made by an end user or Help Desk user. |
| Audit Request Source | The site from which the request was initiated. This entry has one of two values: **Self-Service Portal** or **Helpdesk**. |
| Request Status | Status of the request. Valid statuses are Successful (the key was retrieved), or Failed (the key wasn't retrieved). |
| Helpdesk User | Help Desk user who initiated the request for key retrieval. <br> **Note:** If an Advanced Helpdesk User recovers the key without specifying the end user, the **End User** field is blank. A standard Helpdesk User must specify the end user, and that user appears in this field. A recovery via the Self-Service Portal lists the requesting end user both in this field and in the **End User** field. |
| End User | End user who initiated the request for key retrieval. |
| Computer | Computer name of the computer that was recovered. |
| Key Type | Type of key that the user requested. The three types of keys that MBAM collects are: <ul><li>Recovery Key Password (used to recover a computer in recovery mode)</li><li>Recovery Key ID (used to recover a computer in recovery mode on behalf of another user)</li><li>TPM Password Hash (used to recover a computer with a locked TPM)</li></ul> |
| Reason Description | The reason that the user requested the specified key type. The reasons are specified in the Drive Recovery and Manage TPM features of the Administration and Monitoring website. The valid entries are user-entered text or one of the following reason codes: <ul><li>Operating System Boot Order changed</li><li>BIOS Changed</li><li>Operating System files changed</li><li>Lost Startup key</li><li>Lost PIN</li><li>TPM Reset</li><li>Lost Passphrase</li><li>Lost Smartcard</li><li>Reset PIN lockout</li><li>Turn on TPM</li><li>Turn off TPM</li><li>Change TPM password</li><li>Clear TPM</li></ul> |

> [!NOTE]
> Report results can be saved to a file by selecting the **Export** button on the **Reports** menu bar.

## Related articles

[Monitoring and reporting BitLocker compliance with MBAM 2.5](monitoring-and-reporting-bitlocker-compliance-with-mbam-25.md)

[Generating MBAM 2.5 stand-alone reports](generating-mbam-25-stand-alone-reports.md)
