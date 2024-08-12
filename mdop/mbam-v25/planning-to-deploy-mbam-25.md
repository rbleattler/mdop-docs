---
title: Planning to deploy MBAM 2.5
description: You should consider the different deployment configurations and prerequisites before you create your deployment plan for Microsoft BitLocker Administration and Monitoring (MBAM).
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Planning to deploy MBAM 2.5

You should consider the different deployment configurations and prerequisites before you create your deployment plan for Microsoft BitLocker Administration and Monitoring (MBAM). This article includes information that can help you gather the necessary information to formulate a deployment plan that best meets your business requirements.

## Review the MBAM 2.5 supported configurations

After preparing your computing environment for the MBAM server and client feature deployment, make sure that you review the supported configurations to confirm that the computers on which you install MBAM meet the minimum hardware and operating system requirements. For more information, see, [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md)

## Plan for MBAM 2.5 server and client deployment

The MBAM server infrastructure depends on a set of server features that can be configured on one or more server computers, based on the requirements of the enterprise. These features can be configured in a distributed configuration across multiple servers.

> [!NOTE]
> An MBAM installation on a single server is recommended only for lab environments.

The MBAM client enables administrators to enforce and monitor BitLocker drive encryption on computers in the enterprise. The BitLocker client can be integrated into an organization by deploying the client through an enterprise software delivery system or by installing the Client on client computers as part of the initial imaging process.

With MBAM, you can encrypt a computer in your organization either before the end user receives the computer, or afterwards by using group policy.

[Planning for MBAM 2.5 server deployment](planning-for-mbam-25-server-deployment.md)

[Planning for MBAM 2.5 client deployment](planning-for-mbam-25-client-deployment.md)
