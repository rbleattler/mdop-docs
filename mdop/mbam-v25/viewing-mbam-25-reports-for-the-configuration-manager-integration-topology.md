---
title: Viewing MBAM 2.5 reports for the Configuration Manager integration topology
description: This article describes the reports that are available when you configure Microsoft BitLocker Administration and Monitoring (MBAM) with the Configuration Manager integration topology.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Viewing MBAM 2.5 reports for the Configuration Manager integration topology

This article describes the reports that are available when you configure Microsoft BitLocker Administration and Monitoring (MBAM) with the Configuration Manager integration topology. The reports show BitLocker compliance for the enterprise and for individual computers and devices that MBAM manages. The reports provide tabular information and charts, and they have filters that let you view data from different perspectives.

In the Configuration Manager integration topology, you view reports from Configuration Manager rather than from the Administration and Monitoring website, except for the **Recovery Audit Report**, which you continue to view from the Administration and Monitoring Website.

For information about MBAM reports for the stand-alone topology, see [Viewing MBAM 2.5 reports for the stand-alone topology](viewing-mbam-25-reports-for-the-stand-alone-topology.md).

## Accessing reports in Configuration Manager

To access the Reports feature in Configuration Manager, use one of the following procedures based on your version.

### System Center 2012 Configuration Manager

1. In the left pane, select the Monitoring workspace.
1. In the tree, expand Overview > Reporting > Reports > MBAM.
1. Select the folder that represents the language in which you want to view reports, and then select the report from the right pane.

### Configuration Manager 2007

1. In the left pane, expand Computer Management > Reporting > Reporting Services > "server name" > Report folders > MBAM.
1. Select the folder that represents the language in which you want to view reports, and then select the report from the right pane.

## Description of reports in Configuration Manager

There are a few minor differences in the reports for the Configuration Manager integration topology and the stand-alone topology. The following sections describe the data in the MBAM reports for the Configuration Manager Integration topology.

### <a href="" id="bkmk-dashboard"></a>BitLocker enterprise compliance dashboard

The BitLocker Enterprise Compliance Dashboard provides the following graphs, which show BitLocker compliance status across the enterprise:

- Compliance Status Distribution

- Non Compliant Errors Distribution

- Compliance Status Distribution by Drive Type

#### Compliance status distribution

This pie chart shows compliance status for computers within the enterprise. It also shows the percentage of computers, compared to the total number of computers in the selected collection, that has that compliance status. The actual number of computers with each status is also shown. The pie chart shows the following compliance statuses:

- Compliant

- Non Compliant

- User Exempt

- Temporary User Exempt

- Policy Not Enforced

- Unknown. These computers reported a status error, or they're part of the collection, but haven't reported their compliance status. The lack of a compliance status could occur if the computer is disconnected from the organization.

#### Non compliant errors distribution

This pie chart shows the categories of computers in the enterprise that aren't compliant with the BitLocker Drive Encryption policy, and shows the number of computers in each category. Each category percentage is calculated from the total number of noncompliant computers in the collection.

- User postponed encryption

- Unable to find compatible TPM

- System partition not available or large enough

- Policy conflict

- Waiting for TPM auto provisioning

- An unknown error occurred

- No information. These computers don't have the MBAM Client installed, or they have the MBAM Client installed but not activated (for example, the service isn't working).

#### Compliance status distribution by drive type

This bar chart shows the current BitLocker compliance status by drive type. The statuses are **Compliant** and **Non Compliant**. Bars are shown for fixed data drives and operating system drives. Computers that don't have a fixed data drive are included and show a value only in the **Operating System Drive** bar. The chart doesn't include users who are granted an exemption from the BitLocker Drive Encryption policy or the No Policy category.

### <a href="" id="bkmk-compliancedetails"></a>BitLocker enterprise compliance details

This report shows information about the overall BitLocker compliance across your enterprise for the collection of computers that is targeted for BitLocker use.

#### BitLocker enterprise compliance details fields

| Column Name | Description |
|--|--|
| Managed Computers | Number of computers that MBAM manages. |
| % Compliant | Percentage of compliant computers in the enterprise. |
| % Non-Compliant | Percentage of noncompliant computers in the enterprise. |
| % Unknown Compliance | Percentage of computers with a compliance state that isn't known. |
| % Exempt | Percentage of computers exempt from the BitLocker encryption requirement. |
| % Non-Exempt | Percentage of computers not exempt from the BitLocker encryption requirement. |
| Compliant | Percentage of compliant computers in the enterprise. |
| Non-Compliant | Percentage of noncompliant computers in the enterprise. |
| Unknown Compliance | Percentage of computers with a compliance state that isn't known. |
| Exempt | Total computers that are exempt from the BitLocker encryption requirement. |
| Non-Exempt | Total computers that aren't exempt from the BitLocker encryption requirement. |

#### BitLocker enterprise compliance details states

| Compliance Status | Exemption | Description |
|--|--|--|
| Noncompliant | Not exempt | The computer is noncompliant, according to the specified policy. |
| Compliant | Not exempt | The computer is compliant in accordance with the specified policy. |

### <a href="" id="bkmk-compliancesummary"></a>BitLocker enterprise compliance summary

Use this report type to show information about the overall BitLocker compliance across your enterprise and to show the compliance for individual computers that are in the collection of computers that is targeted for BitLocker use.

#### BitLocker enterprise compliance summary fields

| Column Name | Description |
|--|--|
| Managed Computers | Number of computers that MBAM manages. |
| % Compliant | Percentage of compliant computers in the enterprise. |
| % Non-Compliant | Percentage of noncompliant computers in the enterprise. |
| % Unknown Compliance | Percentage of computers with a compliance state that isn't known. |
| % Exempt | Percentage of computers exempt from the BitLocker encryption requirement. |
| % Non-Exempt | Percentage of computers not exempt from the BitLocker encryption requirement. |
| Compliant | Percentage of compliant computers in the enterprise. |
| Non-Compliant | Percentage of noncompliant computers in the enterprise. |
| Unknown Compliance | Percentage of computers with a compliance state that isn't known. |
| Exempt | Total computers that are exempt from the BitLocker encryption requirement. |
| Non-Exempt | Total computers that aren't exempt from the BitLocker encryption requirement. |

#### BitLocker enterprise compliance summary computer details

| Column Name | Description |
|--|--|
| Computer Name | User-specified DNS computer name that MBAM manages. |
| Domain Name | Fully qualified domain name, where the client computer resides and MBAM manages. |
| Compliance Status | Overall compliance status of the computer managed by MBAM. Valid states are Compliant and Noncompliant. Notice that the compliance status per drive (see the table that follows) might indicate different compliance states. However, this field represents that compliance state, in accordance with the policy specified. |
| Exemption | Status that indicates whether the user is exempt or nonexempt from the BitLocker policy. |
| Device Users | User of the device. |
| Compliance Status Details | Error and status messages about the compliance state of the computer in accordance with the policy specified. |
| Last Contact | Date and time that the computer last contacted the server to report compliance status. The contact frequency is configurable through the group policy settings. |

### <a href="" id="bkmk-compliancereport"></a>BitLocker computer compliance report

Use this report type to collect information that is specific to a computer. The BitLocker Computer Compliance Report provides detailed encryption information about each drive on a computer (operating system and fixed data drives). It also provides an indication of the policy that is applied to each drive type on the computer. To view the details of each drive, expand the Computer Name entry.

> [!NOTE]
> This report doesn't show the Removable Data Volume encryption status.

#### BitLocker Computer Compliance Report: Computer Details Fields**

| Column Name | Description |
|--|--|
| Computer Name | User-specified DNS computer name that MBAM manages. |
| Domain Name | Fully qualified domain name, where the client computer resides and MBAM manages. |
| Computer Type | Type of computer. Valid types are Non-Portable and Portable. |
| Operating System | Operating System type found on the MBAM managed client computer. |
| Overall Compliance | Overall compliance status of the computer managed by MBAM. Valid states are Compliant and Noncompliant. Notice that the compliance status per drive (see the table that follows) might indicate different compliance states. However, this field represents that compliance state in accordance with the policy specified. |
| Operating System Compliance | Compliance status of the operating system that MBAM manages. Valid states are Compliant and Noncompliant. |
| Fixed Data Drive Compliance | Compliance status of the fixed data drive that MBAM manages. Valid states are Compliant and Noncompliant. |
| Last Update Date | Date and time that the computer last contacted the server to report compliance status. The contact frequency is configurable through the group policy settings. |
| Exemption | Status that indicates whether the user is exempt or nonexempt from the BitLocker policy. |
| Exempted User | User who is exempt from the BitLocker policy. |
| Exemption Date | Date on which the exemption was granted. |
| Compliance Status Details | Error and status messages about the compliance state of the computer in accordance with the policy specified. |
| Policy Cipher Strength | Cipher strength selected by the Administrator during the MBAM policy specification (for example, 128-bit with diffuser). |
| Policy: Operating System Drive | Indicates if encryption is required for the operating system and the appropriate protector type. |
| Policy: Fixed Data Drive | Indicates if encryption is required for the fixed data drive. |
| Manufacturer | Computer manufacturer name as it appears in the computer BIOS. |
| Model | Computer manufacturer model name as it appears in the computer BIOS. |
| Device Users | Known users on the computer that MBAM manages. |

#### BitLocker computer compliance report: Computer volume fields

| Column Name | Description |
|--|--|
| Drive Letter | Computer drive letter that the user assigned to the particular drive. |
| Drive Type | Type of drive. Valid values are Operating System Drive and Fixed Data Drive. These drives are physical rather than logical volumes. |
| Cipher Strength | Cipher strength selected by the Administrator during MBAM policy specification. |
| Protector Types | Type of protector selected through the policy used to encrypt an operating system or fixed data drive. The valid protector types for an operating system are TPM or TPM+PIN. The valid protector type for a fixed data drive is a password. |
| Protector State | Indicates that the managed computer enabled the protector type specified in the policy. The valid states are ON or OFF. |
| Encryption State | Encryption state of the drive. Valid states are Encrypted, Not Encrypted, and Encrypting. |

## Related articles

[Monitoring and reporting BitLocker compliance with MBAM 2.5](monitoring-and-reporting-bitlocker-compliance-with-mbam-25.md)
