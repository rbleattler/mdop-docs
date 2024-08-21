---
title: How to use the Administration and Monitoring website
description: The Administration and Monitoring website, also referred to as the Help Desk, is an administrative interface for BitLocker Drive Encryption.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to use the Administration and Monitoring website

The Administration and Monitoring website, also referred to as the Help Desk, is an administrative interface for BitLocker Drive Encryption. Use the website to review reports, recover end users' drives, and manage end users' TPMs, as described in the following sections.

> [!NOTE]
> If you use MBAM in the stand-alone topology, you view all reports from the Administration and Monitoring website. If you use the Configuration Manager integration topology, you view all reports in Configuration Manager. The only exception with Configuration Manager is the Recovery Audit report, which you continue to view from the Administration and Monitoring website. For more information about reports, see [Monitoring and reporting BitLocker compliance with MBAM 2.5](monitoring-and-reporting-bitlocker-compliance-with-mbam-25.md).

## Required roles for using the Administration and Monitoring website

To access specific areas of the Administration and Monitoring website, you must have one of the following roles, which are groups that you create in Active Directory. You can use any name for these groups.

| Account | Description |
|--|--|
| MBAM Advanced Helpdesk Users | Provides access to all areas of the Administration and Monitoring website. Users who have this role enter only the recovery key, and not the end user's domain and user name, when helping end users recover their drives. If a user is a member of both the MBAM Helpdesk Users group and the MBAM Advanced Helpdesk Users group, the MBAM Advanced Helpdesk Users group permissions override the MBAM Helpdesk Users Group permissions. |
| MBAM Helpdesk Users | Provides access to the Manage TPM and Drive Recovery areas of the Administration and Monitoring website. Individuals who have this role must fill in all fields, including the end-user's domain and account name, when they use either area. If a user is a member of both the MBAM Helpdesk Users group and the MBAM Advanced Helpdesk Users group, the MBAM Advanced Helpdesk Users group permissions override the MBAM Helpdesk Users Group permissions. |
| MBAM Report Users | Provides access to the reports in the **Reports** area of the Administration and Monitoring website. |

## Tasks you can perform on the Administration and Monitoring website

The following table summarizes the tasks you can perform on the Administration and Monitoring website and provides links to more information about each task.

| Task | Area of the website where you access the task | Description | For more information |
|--|--|--|--|
| View reports | Reports | Enables you to run reports to monitor BitLocker usage, compliance, and key recovery activity. Reports provide data about enterprise compliance, individual computers, and who requested recovery keys or the TPM OwnerAuth package for a specific computer. | [Viewing MBAM 2.5 reports for the stand-alone topology](viewing-mbam-25-reports-for-the-stand-alone-topology.md) |
| Determine the BitLocker encryption status of lost or stolen computers | Reports | Determine if a volume was encrypted if the computer is lost or stolen. | [How to Determine BitLocker encryption state of lost computers](how-to-determine-bitlocker-encryption-state-of-lost-computers-mbam-25.md) |
| Recover lost drives | Drive Recovery | Recover drives that are: <ul><li>In recovery mode</li><li>Have been moved</li><li>Are corrupted</li></ul> | <ul><li>[How to recover a drive in recovery mode](how-to-recover-a-drive-in-recovery-mode-mbam-25.md)</li><li>[How to recover a moved drive](how-to-recover-a-moved-drive-mbam-25.md)</li><li>[How to recover a corrupted drive](how-to-recover-a-corrupted-drive-mbam-25.md)</li></ul> |
| Reset a TPM lockout | Manage TPM | Provides access to TPM data that has been collected by the MBAM Client. In a TPM lockout, use the Administration and Monitoring website to retrieve the necessary password file to unlock the TPM. | [How to reset a TPM lockout](how-to-reset-a-tpm-lockout-mbam-25.md) |

## Related articles

[Performing BitLocker management with MBAM 2.5](performing-bitlocker-management-with-mbam-25.md)
