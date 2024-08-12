---
title: Removing MBAM server features or software
description: These instructions explain how to remove software and features from Microsoft BitLocker Administration and Monitoring (MBAM).
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Removing MBAM server features or software

These instructions explain how to remove software and features from Microsoft BitLocker Administration and Monitoring (MBAM). If you remove MBAM server features, only the configured features are removed from the server, not the MBAM server software. If you remove the MBAM server software, the software and any MBAM server features that you configured on that server are removed.

> [!NOTE]
> To prevent the accidental removal of data, MBAM provides no mechanism for removing the databases. You must do that action manually.

## <a href="" id="bkmk-removeserverfeatures"></a>Removing MBAM server features

You can use either of the following methods to remove MBAM server features that you configured:

- MBAM server Configuration wizard

- Windows PowerShell cmdlets

### Using the MBAM server Configuration wizard to remove features

Follow these instructions to use the MBAM server Configuration wizard to remove configured MBAM server features from a server.

#### To remove MBAM features by using the wizard

1.  On the server where you want to remove features, select **MBAM server Configuration** to open the configuration wizard.

2.  Select **Remove Features**, select the features to remove, and then select **Next**. A **Summary** page displays the features you selected for removal.

3.  Select **Remove** to start removing the features, and then select **Close**.

### Using Windows PowerShell to remove features

To remove MBAM server features by using Windows PowerShell cmdlets, use the following steps as a general guide.

#### To remove MBAM features by using Windows PowerShell

1.  Before removing any features, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md) to review the prerequisites for using Windows PowerShell.

2.  Use the following cmdlets to remove MBAM server features:

    - Disable-MbamReport

    - Disable-MbamWebApplication

    - Disable-MbamCMIntegration

    To get help with Windows PowerShell cmdlets, type `Get-Help <cmdletName>`. For more information on the MBAM Windows PowerShell cmdlets, see [Microsoft Desktop Optimization Pack automation with Windows PowerShell](/powershell/mdop/get-started).

## Removing MBAM server software

Use the following steps to remove the MBAM server software and any MBAM server features that you configured on that server.

### To remove the MBAM server software

1.  On the server where you want to uninstall the MBAM server software, run **MBAMserversetup.exe** to start the Microsoft BitLocker Administration and Monitoring Setup wizard.

2.  Select **Uninstall**, and follow the remaining prompts to complete the process of uninstalling the MBAM server software.

## Related articles

[MBAM 2.5 deployment checklist](mbam-25-deployment-checklist.md)
