---
title: Deploy the MBAM client to desktop and laptop computers
description: This article explains how to deploy the MBAM client to users' computers.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Deploy the MBAM client to desktop and laptop computers

This article explains how to deploy the MBAM client to users' computers. You can deploy the MBAM client through an electronic software distribution system, such as Active Directory Domain Services or Microsoft System Center Configuration Manager.

To deploy the MBAM client as part of a Windows deployment, see [How to enable BitLocker by using MBAM as part of a Windows deployment](how-to-enable-bitlocker-by-using-mbam-as-part-of-a-windows-deploymentmbam-25.md).

Before you start the MBAM client deployment, review the [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).

## To deploy the MBAM client to desktop or laptop computers

1.  Locate the MBAM client installation files that are provided with the MBAM software.

2.  To deploy the Windows Installer package to target computers, use Active Directory Domain Services or an enterprise software deployment tool like Microsoft System Center Configuration Manager.

3.  Configure the distribution settings or Group Policy settings to run the MBAM client installation file.

    After successful installation, the MBAM client applies the Group Policy settings that are received from a domain controller to begin BitLocker Drive Encryption and management functions.

    > [!IMPORTANT]
    > If a remote desktop protocol connection is active, the MBAM client doesn't start BitLocker Drive Encryption actions. Before BitLocker Drive Encryption begins, all remote console connections must be closed and a user must be signed in to a physical console session.

## Related articles

[Deploying the MBAM 2.5 client](deploying-the-mbam-25-client.md)

[Planning for MBAM 2.5 client deployment](planning-for-mbam-25-client-deployment.md)
