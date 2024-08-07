---
title: Deploying the MBAM 2.5 client
description: The Microsoft BitLocker Administration and Monitoring (MBAM) client software enables administrators to enforce and monitor BitLocker Drive Encryption on computers in the enterprise.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Deploying the MBAM 2.5 client

The Microsoft BitLocker Administration and Monitoring (MBAM) client software enables administrators to enforce and monitor BitLocker Drive Encryption on computers in the enterprise. The BitLocker client can be integrated into an organization by deploying the client through an electronic software distribution system, such as Active Directory Domain Services, or by directly encrypting the client computers as part of the initial imaging process.

Depending on when you deploy the Microsoft BitLocker Administration and Monitoring Client software, you can enable BitLocker Drive Encryption on a computer in your organization either before the end user receives the computer or afterwards by configuring group policy and deploying the  MBAM client software by using an enterprise software deployment system.

## Deploy the MBAM client to desktop or laptop computers

After configuring group policy settings, you can use an enterprise software deployment system product like Microsoft System Center 2012 Configuration Manager or Active Directory Domain Services to deploy the  MBAM client installation Windows Installer files to target computers. You can use either the 32-bit or 64-bit MbamClientSetup.exe files or the 32-bit or 64-bit MBAMClient.msi files, which are provided with the  MBAM client software. For more information about deploying MBAM group policy settings, see [Deploying MBAM 2.5 group policy objects](deploying-mbam-25-group-policy-objects.md).

> [!NOTE]
> Beginning in MBAM 2.5 SP1, a separate MSI is no longer included with the MBAM product. However, you can extract the MSI from the executable file (.exe) that is included with the product.

[How to deploy the MBAM client to desktop or laptop computers](how-to-deploy-the-mbam-client-to-desktop-or-laptop-computers-mbam-25.md)

## Deploy the  MBAM client as part of a Windows deployment

In organizations where computers are received and configured centrally, you can install the  MBAM client to manage BitLocker Drive Encryption on each computer before any user data is written to it. The benefit of this process is that every computer is then BitLocker Drive Encryption-compliant. This method doesn't rely on user action because the administrator has already encrypted the computer. A key assumption for this scenario is that the policy of the organization installs a corporate Windows image before the computer is delivered to the user. If the group policy settings are configured to require a PIN, users are prompted to set a PIN after they receive the policy.

[How to enable BitLocker by using MBAM as part of a Windows deployment](how-to-enable-bitlocker-by-using-mbam-as-part-of-a-windows-deploymentmbam-25.md)

## How to deploy the  MBAM client by using a command line

This section explains how to install the  MBAM client by using a command line.

[How to deploy the MBAM client by using a command line](how-to-deploy-the-mbam-client-by-using-a-command-line.md)

## Related articles

[MBAM 2.5 planning checklist](mbam-25-planning-checklist.md)

[MBAM 2.5 deployment checklist](mbam-25-deployment-checklist.md)
