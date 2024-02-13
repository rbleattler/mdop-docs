---
title: Microsoft BitLocker Administration and Monitoring 2.5
description: Microsoft BitLocker Administration and Monitoring 2.5
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
manager: aaroncz
ms.topic: article
ms.date: 04/19/2017
---

# Microsoft BitLocker Administration and Monitoring 2.5

> [!WARNING]
> MBAM mainstream support ended on July 2019 and is currently in extended support until April 2026

Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 provides a simplified administrative interface that you can use to manage BitLocker Drive Encryption. You configure MBAM Group Policy Templates that enable you to set BitLocker Drive Encryption policy options that are appropriate for your enterprise, and then use them to monitor client compliance with those policies. You can also report on the encryption status of an individual computer and on the enterprise as a whole. In addition, you can access recovery key information when users forget their PIN or password or when their BIOS or boot record changes. For a more detailed description of MBAM, see [About MBAM 2.5](about-mbam-25.md).

> [!IMPORTANT]
> Enterprises can use Microsoft BitLocker Administration and Monitoring (MBAM) to manage client computers with BitLocker that are domain-joined on-premises until mainstream support ends in July 2019 or they can receive extended support until April 2026. Customers who are in extended support can obtain MBAM by seeing [How Do I Get MDOP](/microsoft-desktop-optimization-pack/index#how-to-get-mdop).
>
> Going forward, the functionality of MBAM has been incorporated into Microsoft Configuration Manager as **Microsoft Configuration Manager BitLocker Management**. For more information, see [Plan for BitLocker management](/mem/configmgr/protect/plan-design/bitlocker-management).
>
> Customers not using Microsoft Configuration Manager can utilize the built-in features of Microsoft Entra ID and Microsoft Intune for administration and monitoring of BitLocker. For more information, see [Manage BitLocker policy for Windows devices with Intune](/mem/intune/protect/encrypt-devices).


## Outline

- <a href="" id="getting-started-with-mbam-2-5"></a>[Getting Started with MBAM 2.5](getting-started-with-mbam-25.md)
  - [About MBAM 2.5](about-mbam-25.md)
  - [Release Notes for MBAM 2.5](release-notes-for-mbam-25.md)
  - [About MBAM 2.5 SP1](about-mbam-25-sp1.md)
  - [Release Notes for MBAM 2.5 SP1](release-notes-for-mbam-25-sp1.md)
  - [Evaluating MBAM 2.5 in a Test Environment](evaluating-mbam-25-in-a-test-environment.md)
  - [High-Level Architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md)
  - [Accessibility for MBAM 2.5](accessibility-for-mbam-25.md)
- <a href="" id="planning-for-mbam-2-5"></a>[Planning for MBAM 2.5](planning-for-mbam-25.md)
  - [Preparing your Environment for MBAM 2.5](preparing-your-environment-for-mbam-25.md)
  - [MBAM 2.5 Deployment Prerequisites](mbam-25-deployment-prerequisites.md)
  - [Planning for MBAM 2.5 Group Policy Requirements](planning-for-mbam-25-group-policy-requirements.md)
  - [Planning for MBAM 2.5 Groups and Accounts](planning-for-mbam-25-groups-and-accounts.md)
  - [Planning How to Secure the MBAM Websites](planning-how-to-secure-the-mbam-websites.md)
  - [Planning to Deploy MBAM 2.5](planning-to-deploy-mbam-25.md)
  - [MBAM 2.5 Supported Configurations](mbam-25-supported-configurations.md)
  - [Planning for MBAM 2.5 High Availability](planning-for-mbam-25-high-availability.md)
  - [MBAM 2.5 Security Considerations](mbam-25-security-considerations.md)
  - [MBAM 2.5 Planning Checklist](mbam-25-planning-checklist.md)
- <a href="" id="deploying-mbam-2-5"></a>[Deploying MBAM 2.5](deploying-mbam-25.md)
  - [Deploying the MBAM 2.5 Server Infrastructure](deploying-the-mbam-25-server-infrastructure.md)
  - [Deploying MBAM 2.5 Group Policy Objects](deploying-mbam-25-group-policy-objects.md)
  - [Deploying the MBAM 2.5 Client](deploying-the-mbam-25-client.md)
  - [MBAM 2.5 Deployment Checklist](mbam-25-deployment-checklist.md)
  - [Upgrading to MBAM 2.5 or MBAM 2.5 SP1 from Previous Versions](upgrading-to-mbam-25-or-mbam-25-sp1-from-previous-versions.md)
  - [Removing MBAM Server Features or Software](removing-mbam-server-features-or-software.md)
- <a href="" id="operations-for-mbam-2-5"></a>[Operations for MBAM 2.5](operations-for-mbam-25.md)
  - [Administering MBAM 2.5 Features](administering-mbam-25-features.md)
  - [Monitoring and Reporting BitLocker Compliance with MBAM 2.5](monitoring-and-reporting-bitlocker-compliance-with-mbam-25.md)
  - [Performing BitLocker Management with MBAM 2.5](performing-bitlocker-management-with-mbam-25.md)
  - [Maintaining MBAM 2.5](maintaining-mbam-25.md)
  - [Using Windows PowerShell to Administer MBAM 2.5](using-windows-powershell-to-administer-mbam-25.md)
- <a href="" id="troubleshooting-mbam-2-5"></a>[Troubleshooting MBAM 2.5](troubleshooting-mbam-25.md)
- <a href="" id="technical-reference-for-mbam-2-5"></a>[Technical Reference for MBAM 2.5](technical-reference-for-mbam-25.md)
  - [Client Event Logs](client-event-logs.md)
  - [Server Event Logs](server-event-logs.md)

## More Information

- [MDOP Information Experience](index.md)

  Find documentation, videos, and other resources for MDOP technologies.

- [MBAM Deployment Guide](https://www.microsoft.com/download/details.aspx?id=38398)

  Get help in choosing a deployment method for MBAM, including step-by-step instructions for each method.
    
- [Apply Hotfixes on MBAM 2.5 SP1 Server](apply-hotfix-for-mbam-25-sp1.md)

  Guide of how to apply MBAM 2.5 SP1 Server hotfixes
