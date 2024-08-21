---
title: How to deploy the MBAM client by using a command line
description: You can use a command line to deploy the Microsoft BitLocker Administration and Monitoring (MBAM) client software.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to deploy the MBAM client by using a command line

You can use a command line to deploy the Microsoft BitLocker Administration and Monitoring (MBAM) client software.

## Command line to deploy the MBAM client software

To automatically accept the end user license agreement when deploying the MBAM client software, type the following command at the command prompt:

`MBAMClientSetup.exe /acceptEula=Yes`

> [!NOTE]
> The `/ju` and `/jm` command-line options aren't supported and can't be used to install the MBAM client software.

To extract and install the MSP, type the following command at the command prompt:

`MBAMClientSetup.exe /extract <path to extract MSI> /acceptEula=Yes`

Then, install the MSI silently by running the following command:

`msiexec /i <path to extracted MSI> /qb ALLUSERS=1 REBOOT=ReallySuppress`

> [!NOTE]
> Beginning in MBAM 2.5 SP1, a separate MSI is no longer included with the MBAM product. However, you can extract the MSI from the executable file (.exe) that's included with the product, after accepting the EULA.

## <a href="" id="optin-for-microsoft-updates-1-command-line-option"></a> `OPTIN_FOR_MICROSOFT_UPDATES=1` command-line option

You can optionally specify the command-line option `OPTIN_FOR_MICROSOFT_UPDATES=1` during the client software installation to automatically install Microsoft Updates on client computers. Specifying this option makes Microsoft Update automatically start and search for available updates to install after the client software installation finishes.

You can use this command-line option with either of the following installation methods.

| Install the MBAM client software by using | Example                                                   |
|-------------------------------------------|-----------------------------------------------------------|
| `MBAMClientSetup.exe`                   | `MbamClientSetup.exe OPTIN_FOR_MICROSOFT_UPDATES=1`     |
| `msiexec /i MBAMClient.msi`             | `msiexec /i MBAMClient.msi OPTIN_FOR_MICROSOFT_UPDATES=1` |

## Related articles

[Deploying the MBAM 2.5 client](deploying-the-mbam-25-client.md)
