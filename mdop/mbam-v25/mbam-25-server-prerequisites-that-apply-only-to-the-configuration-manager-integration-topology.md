---
title: MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology
description: If you install Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 by using the System Center Configuration Manager integration feature, you must complete the prerequisites described in this article
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology

If you install Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 by using the System Center Configuration Manager integration feature, you must complete the prerequisites described in this article, in addition to those in [MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md). You must also create or modify .mof files that are needed for the Configuration Manager Integration topology.

## Prerequisites for the Configuration Manager integration feature

If you configure MBAM with the System Center Configuration Manager integration topology, you must complete other prerequisites that are required for Configuration Manager.

[Prerequisites for the Configuration Manager integration Feature](prerequisites-for-the-configuration-manager-integration-feature.md)

## Edit the configuration.mof file

To enable the client computers to report BitLocker compliance details through the MBAM Configuration Manager Reports, you have to edit the Configuration.mof file for System Center 2012 Configuration Manager and Microsoft System Center Configuration Manager 2007.

[Edit the configuration.mof file](edit-the-configurationmof-file-mbam-25.md)

## <a href="" id="create-or-edit-the-sms-def-mof-file"></a>Create or edit the Sms\_def.mof file

To enable the client computers to report BitLocker compliance details in the MBAM Configuration Manager Reports, you have to create or edit the Sms\_def.mof file. If you use System Center 2012 Configuration Manager, you must create the file. In Configuration Manager 2007, the file already exists, so you need to edit, but not overwrite, the existing file.

[Create or edit the sms\_def.mof file](create-or-edit-the-sms-defmof-file-mbam-25.md)

## Related articles

[Preparing your environment for MBAM 2.5](preparing-your-environment-for-mbam-25.md)

[MBAM 2.5 supported configurations](mbam-25-supported-configurations.md)

[Planning to deploy MBAM 2.5](planning-to-deploy-mbam-25.md)
