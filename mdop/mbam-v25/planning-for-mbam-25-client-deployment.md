---
title: Planning for MBAM 2.5 client deployment
description: Depending on when you deploy the Microsoft BitLocker Administration and Monitoring (MBAM) client software, you can enable BitLocker Drive Encryption on a computer in your organization either before the user receives the computer or afterwards.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Planning for MBAM 2.5 client deployment

Depending on when you deploy the Microsoft BitLocker Administration and Monitoring (MBAM) client software, you can enable BitLocker Drive Encryption on a computer in your organization either before the user receives the computer or afterwards. For both the MBAM stand-alone and the System Center Configuration Manager integration topologies, you have to configure group policy settings for MBAM.

If you use the MBAM stand-alone topology, we recommend that you use an enterprise software deployment system to deploy the MBAM client software to user computers.

If you deploy MBAM with the Configuration Manager integration topology, you can use Configuration Manager to deploy the MBAM client software to user computers. In Configuration Manager, the MBAM installation creates a collection of computers that MBAM can manage. This collection includes workstations and devices that don't have a Trusted Platform Module (TPM), but that are running Windows 8, Windows 8.1, or Windows 10.

## Deploying the MBAM client to enable BitLocker Drive Encryption after computer distribution to users

After you configure group policy, you can use an enterprise software deployment system product like Microsoft System Center Configuration Manager or Active Directory Domain Services to deploy the Windows Installer files of the MBAM client installation to target computers. To deploy the MBAM client, you can use either the 32-bit or 64-bit MbamClientSetup.exe files or MBAMClient.msi files, which are provided with the MBAM client software.

> [!NOTE]
> Beginning in MBAM 2.5 SP1, a separate MSI is no longer included with the MBAM product. However, you can extract the MSI from the executable file (.exe) that's included with the product.

When you deploy the MBAM client after you distribute computers to client computers, users are prompted to encrypt their computer. This action enables MBAM to collect the data, which includes the PIN and password (if required by policy), and then to begin the encryption process.

> [!NOTE]
> If the TPM chip isn't already activated, the device prompts the user to activate and initialize the TPM chip.

## Using the MBAM client to enable BitLocker Drive Encryption before computer distribution to users

In organizations where computers are received and configured centrally, and where computers have a compliant TPM chip, you can use the MBAM client to manage BitLocker Drive Encryption on each computer before any user data is written to it. The benefit of this process is that every computer is then compliant. This method doesn't rely on end-user action because the administrator has already encrypted the computer. A key assumption for this scenario is that the policy of the organization installs a corporate Windows image before the computer is delivered to the user.

If your organization wants to use the TPM chip to encrypt computers, the administrator adds the TPM protector to encrypt the operating system volume of the computer. If your organization wants to use the TPM chip and a PIN protector, the administrator encrypts the operating system volume with the TPM protector, and then users select a PIN when they sign in for the first time. If your organization decides to use only the PIN protector, the administrator doesn't have to encrypt the volume first. When users sign in, MBAM prompts them to provide a PIN, or a PIN and password to be used on later computer restarts.

> [!NOTE]
> The TPM protector option requires the administrator to accept the BIOS prompt to activate and initialize the TPM before the computer is delivered to the user.

## MBAM client support for encrypted hard drives

MBAM supports BitLocker on Encrypted Hard Drives that meet TCG specification requirements for Opal and IEEE 1667 standards. When BitLocker is enabled on these devices, it generates keys and does management functions on the encrypted drive. For more information, see [Encrypted hard drive](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831627(v=ws.11)).

## Related articles

[Planning to deploy MBAM 2.5](planning-to-deploy-mbam-25.md)

[Deploying the MBAM 2.5 client](deploying-the-mbam-25-client.md)
