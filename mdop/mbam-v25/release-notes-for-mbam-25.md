---
title: Release Notes for MBAM 2.5
description: Release Notes for MBAM 2.5
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.prod: w10
ms.date: 08/30/2016
---


# Release Notes for MBAM 2.5

Read these release notes thoroughly before you install Microsoft BitLocker Administration and Monitoring (MBAM) 2.5. These release notes contain information that is required to successfully install MBAM and can contain information that isn't available in the product documentation. If these release notes differ from other MBAM 2.5 documentation, consider the latest change to be authoritative. These release notes supersede the content that is included with this product.

## MBAM 2.5 known issues

This section contains release notes for MBAM 2.5.

### Web browser unintentionally run as administrator

Help links in the MBAM Server Configuration tool can cause browser windows to open with administrator rights.

**Workaround:** Enable Internet Explorer Enhanced Security Configuration (IESC) or close your web browser before navigating to other sites.

> [!NOTE]
> This is fixed in MBAM 2.5 SP1.

### MBAM reports as noncompliant a client encrypted with AES 256-bit encryption keys and Diffuser

If a computer has the MBAM 2.5 client installed and is encrypted by using the AES 256-bit with Diffuser cipher strength, the MBAM client is reported as noncompliant in the MBAM compliance reports.

**Workaround:** Install the [Hotfix Package 1 for Microsoft BitLocker Administration and Monitoring 2.5](https://support.microsoft.com/topic/hotfix-package-1-for-microsoft-bitlocker-administration-and-monitoring-2-5-48e14840-2d8e-fbbc-2942-60066889e237).

### MBAM fails to encrypt a volume and reports an error if you set a TPM + PIN protector on a tablet device

If end users try to set a TPM + PIN protector on a tablet device, MBAM fails to encrypt, and it reports an error. This issue occurs because tablet devices don't have a preboot environment keyboard.

**Workaround:** Enable the **Enable use of BitLocker authentication requiring preboot keyboard input on tablets** Group Policy setting. This setting is a BitLocker Group Policy setting and isn't available in the MBAM Group Policy Templates.

### User principal name is required for all service accounts

A user principal name (UPN) must be set for all service accounts in MBAM. If you fail to create a UPN for an account, an error message appears during the configuration process to indicate that the user or group couldn't be found in Active Directory.

**Workaround:** Add the UPN to the service account.

### Self-Service Portal requires additional configuration if client computers can't access Microsoft Ajax Content Delivery Network

If your client computers don't have access to the Microsoft Ajax Content Delivery Network (CDN), which gives the Self-Service Portal the access that it requires to certain JavaScript files, you must configure the Self-Service Portal to reference the JavaScript files from an accessible source. If you don't configure the Self-Service Portal when client computers can't access CDN, only the company name and the account under which you logged on is displayed. No error message appears.

**Workaround:** Install MBAM 2.5 SP1. or configure the Self-Service Portal by following these instructions: [How to Configure the Self-Service Portal When Client Computers Can't Access the Microsoft Content Delivery Network](how-to-configure-the-self-service-portal-when-client-computers-cannot-access-the-microsoft-content-delivery-network.md).

### Self-Service Portal and the Administration and Monitoring Website don't open after you upgrade IIS to .NET Framework 4.5

When you upgrade Internet Information Services (IIS) to the Microsoft .NET Framework 4.5, the Self-Service Portal and the Administration and Monitoring Website don't open.

**Workaround:** See the article **Error message after you install the .NET Framework 4.0: "Could not load type 'System.ServiceModel.Activation.HttpModule'**.

### Administration and Monitoring Website displays a "Report can't be found" error message when Reports aren't configured

If you configure the Administration and Monitoring Website and then try to view a report without configuring the Reports feature first, an error message indicates that the report can't be found.

**Workaround:** Configure the Reports feature before you configure the web applications.

### Reports in the Administration and Monitoring Website display a warning if SSL isn't configured in SSRS

If SQL Server Reporting Services (SSRS) wasn't configured to use Secure Socket Layer (SSL), the URL for the Reports feature will be set to HTTP instead of to HTTPS when you configure the MBAM Server. If you then open the Administration and Monitoring Website and select a report, the following error message appears: "Only Secure Content is Displayed."

**Workaround:** To show the report, select **Show All Content**. To correct this issue, go to the MBAM computer where SQL Server Reporting Services is installed, run **Reporting Services Configuration Manager**, and then select **Web Service URL**. Select the appropriate SSL certificate for the server, enter the appropriate SSL port (the default port is 443), and then select **Apply**.

### Clicking "Back" in the BitLocker Compliance Summary report might throw an error

If you drill down into a BitLocker Compliance Summary report, and then select the **Back** link in the SSRS report, an error might be thrown.

**Workaround:** None.

### Used Space Only Encryption doesn't work correctly

If you encrypt a computer for the first time after you install the MBAM Client, and you have configured a Group Policy setting to implement Used Space Only encryption, MBAM erroneously encrypts the entire disk instead of encrypting only the disk's used space. If a computer is already encrypted with Used Space Only when you install the MBAM Client, and you have configured the same Group Policy setting, MBAM reports that the drive is encrypted correctly, and doesn't try to re-encrypt the drive.

**Workaround:** None.

### Cipher strength displays incorrectly on the BitLocker Computer Compliance report

If you don't set a specific cipher strength in the **Choose drive encryption method and cipher strength** Group Policy Object, the BitLocker Computer Compliance report in the Configuration Manager Integration topology always displays "unknown" for the cipher strength, even when the cipher strength uses the default of 128-bit encryption. The report displays the correct cipher strength if you set a specific cipher strength in the Group Policy Object.

**Workaround:** Always set a specific cipher strength in the **Choose drive encryption method and cipher strength** Group Policy Object.

### Compliance Status Distribution by Drive Type displays old data after you update configuration items

After you update MBAM configuration items in System Center 2012 Configuration Manager, the Compliance Status Distribution By Drive Type bar chart on the BitLocker Enterprise Compliance Dashboard shows data that is based on information from old versions of the configuration items.

**Workaround:** None. Modification of the MBAM configuration items isn't supported, and the report might not appear as expected.

### Enhanced Security Configuration might cause reports to display an error message incorrectly

If Internet Explorer Enhanced Security Configuration (ESC) is turned on, an "Access Denied" error message might appear when you try to view reports on the MBAM Server. By default, ESC is turned on to protect the server by decreasing the server's exposure to potential attacks that can occur through web content and application scripts.

**Workaround:** If the "Access Denied" error message appears when you try to view reports on the MBAM Server, you can set a Group Policy Object or change the default manually in your image to disable Enhanced Security Configuration. You can also alternatively view the reports from another computer on which ESC isn't enabled.

## Hotfixes and Knowledge Base articles for MBAM 2.5


This table lists the hotfixes and KB articles for MBAM 2.5.

- 2975636: [Hotfix Package 1 for Microsoft BitLocker Administration and Monitoring 2.5](https://support.microsoft.com/topic/hotfix-package-1-for-microsoft-bitlocker-administration-and-monitoring-2-5-48e14840-2d8e-fbbc-2942-60066889e237)

- 3015477: [Hotfix Package 2 for BitLocker Administration and Monitoring 2.5](https://support.microsoft.com/topic/hotfix-package-2-for-bitlocker-administration-and-monitoring-2-5-8c51765a-99bb-d8ff-f55a-6182f5b674ae)

- 3011022: MBAM 2.5 installation or Configuration Manager reporting fails if the name of SSRS instance contains an underscore

- 2756402: [MBAM client would fail with Event ID 4 and error code 0x8004100E in the Event description](/troubleshoot/windows-client/windows-security/mbam-client-fails-event-id-4-0x8004100e)

- 2639518: [Error opening Enterprise or Computer Compliance Reports in MBAM](/troubleshoot/windows-server/windows-security/error-when-opening-reports-mbam)

- 2870842: MBAM 2.0 Setup fails during Configuration Manager Integration Scenario with SQL Server 2008

- 2975472: [SQL deadlocks when many MBAM clients connect to the MBAM recovery database](https://support.microsoft.com/topic/sql-deadlocks-when-many-mbam-clients-connect-to-the-mbam-recovery-database-314a8c69-449c-f47c-e0bf-310fdf5c63a7)


## Related information

[About MBAM 2.5](about-mbam-25.md)
