---
title: Release Notes for App-V 5.0
description: Release Notes for App-V 5.0
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---


# Release Notes for App-V 5.0

Read these release notes thoroughly before you install App-V 5.0.

These release notes contain information that is required to successfully install App-V 5.0. The release notes also contain information that isn't available in the product documentation. If there's a difference between these release notes and other App-V 5.0 documentation, the latest change should be considered authoritative. These release notes supersede the content that is included with this product.


## Known Issues with App-V 5.0


This section contains release notes about the known issues with App-V 5.0.

### Unable to terminate adding packages when using server PowerShell cmdlets

When you add a package using PowerShell, there's no method to exit adding new packages.

WORKAROUND: To stop adding packages, press **enter** after you have added the final package.

### App-V 5.0 client rejects packages from servers whose certificate has been revoked

When using the HTTPS protocol, the App-V 5.0 client will by default reject packages from servers whose certificate has been revoked. This behavior can be turned off through configuration by modifying the **VerifyCertificateRevocationList** setting. Applying new configuration for this setting won't take effect until the App-V 5.0 service is restarted.

WORKAROUND: Restart the App-V 5.0 service.

## Related information

[About App-V 5.0](about-app-v-50.md)
