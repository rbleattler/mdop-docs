---
title: How to move the MBAM 2.5 websites
description: Use these procedures to move the following MBAM websites from one computer to another.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to move the MBAM 2.5 websites

Use these procedures to move the following MBAM websites from one computer to another. For example, to move the following features from Server A to Server B:

- Administration and Monitoring website

- Self-Service Portal

> [!IMPORTANT]
> During the configuration of both websites, you must provide the same connection string, Reports URL, group accounts, and web service application pool domain account as the ones that you are currently using. If you don't use the same values, you can't access some of the servers. To get the current values, use the **Get-MbamWebApplication** Windows PowerShell cmdlet.

## To move the Administration and Monitoring website to another server

1.  On Server B, install the MBAM 2.5 Server software. For instructions, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).

2.  On Server B, start the MBAM Server Configuration wizard, select **Add New Features**, and then select only the **Administration and Monitoring Website** feature.

    Alternatively, you can use the **Enable-MbamWebApplication** Windows PowerShell cmdlet to configure the Administration and Monitoring Website.

    For instructions on how to configure the Administration and Monitoring Website, see [How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md).

## To move the Self-Service Portal to another server

1.  On Server B, install the MBAM 2.5 Server software. For instructions, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).

2.  On Server B, start the MBAM Server Configuration wizard, select **Add New Features**, and then select only the **Self-Service Portal** feature.

    Alternatively, you can use the **Enable-MbamWebApplication** Windows PowerShell cmdlet to configure the Self-Service Portal.

    For instructions on how to configure the Administration and Monitoring Website, see [How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md).

3.  If the client computers in your organization don't have access to the Microsoft content delivery network, you also have to move the JavaScript files. For more information, see [How to configure the Self-Service Portal when client computers can't access the Microsoft content delivery network](how-to-configure-the-self-service-portal-when-client-computers-cannot-access-the-microsoft-content-delivery-network.md).

4.  Customize the Self-Service Portal for your organization. Use the instructions in [Customizing the Self-Service Portal for your organization](customizing-the-self-service-portal-for-your-organization.md) to review your current customizations and to configure custom settings on the Self-Server Portal on Server B.

## Related articles

[How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md)

[Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md)

[Moving MBAM 2.5 features to another server](moving-mbam-25-features-to-another-server.md)
