---
title: Deploying MBAM with Configuration Manager
description: Deploying MBAM with Configuration Manager
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.date: 08/30/2016
---


# Deploying MBAM with Configuration Manager


The following procedures describe how to deploy Microsoft BitLocker Administration and Monitoring (MBAM) with Microsoft System Center Configuration Manager 2007 or Microsoft System Center 2012 Configuration Manager by using the recommended configuration, which is described in [Getting Started - Using MBAM with Configuration Manager](getting-started---using-mbam-with-configuration-manager.md). The recommended configuration is to install the Administration and Monitoring features on one or more Microsoft BitLocker Administration and Monitoring servers, and install Microsoft System Center Configuration Manager 2007 or Microsoft System Center 2012 Configuration Manager on a separate server.

Before you start the installation, ensure that you have met the prerequisites and hardware and software requirements for installing MBAM with Configuration Manager by reviewing [Planning to Deploy MBAM with Configuration Manager](planning-to-deploy-mbam-with-configuration-manager-2.md).

If you ever have to reinstall MBAM with the Configuration Manager topology, you need to remove certain Configuration Manager objects first.

The steps to install MBAM with Configuration Manager are grouped into the following categories. Complete the steps for each category to complete the installation.

## How to create or edit the `.mof` files


To enable the client computers to report BitLocker compliance details through the MBAM Configuration Manager reports, you have to edit the `Configuration.mof` file, and either edit or create the `sms_def.mof` file, depending on which version of Configuration Manager you're using.

[How to create or edit the `.mof` files](how-to-create-or-edit-the-mof-files.md)

## How to Install MBAM with Configuration Manager


This section provides steps about how to install the following: MBAM on the Configuration Manager Server; the Recovery and Audit Databases on the Database Server; and the Administration and Monitoring Server features on the Administration and Monitoring Server.

[How to Install MBAM with Configuration Manager](how-to-install-mbam-with-configuration-manager.md)

## How to Validate the MBAM Server Feature Installation on the Configuration Manager Server


When the Microsoft BitLocker Administration and Monitoring installation is complete, validate that the installation has successfully set up all the necessary MBAM features required for the Configuration Manager Server.

[How to Validate the MBAM Installation with Configuration Manager](how-to-validate-the-mbam-installation-with-configuration-manager.md)

## Related information

[Using MBAM with Configuration Manager](using-mbam-with-configuration-manager.md)
