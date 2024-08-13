---
title: How to enable BitLocker by using MBAM as part of a Windows deployment
description: This article explains how to enable BitLocker on a user's computer by using Microsoft BitLocker Administration and Monitoring (MBAM) as part of your Windows imaging and deployment process.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/08/2024
---

# How to enable BitLocker by using MBAM as part of a Windows deployment

> [!IMPORTANT]
> These instructions don't apply to Configuration Manager BitLocker Management. The `Invoke-MbamClientDeployment.ps1` PowerShell script isn't supported for use with BitLocker Management in Configuration Manager. This includes escrowing of BitLocker recovery keys during a Configuration Manager task sequence.
>
> Starting with Configuration Manager, version 2103, Configuration Manager BitLocker Management no longer uses the MBAM key recovery services site to escrow keys. Attempting to use the `Invoke-MbamClientDeployment.ps1` PowerShell script with Configuration Manager, version 2103 or later can result in serious problems with the Configuration Manager site. Known problems include creation of a large amount of policy targeted to all devices, which can cause policy storms. This behavior leads to severe degradation of performance in Configuration Manager primarily in SQL and with management points. For more information, see [Using the MBAM agent to escrow BitLocker recovery keys generates excessive policies in Configuration Manager, version 2103](/mem/configmgr/hotfix/2103/10372804).
>
> BitLocker Management starting with Configuration Manager, version 2203 natively supports escrowing the BitLocker key during a task sequence with the **Enable BitLocker** task sequence task via the option **Automatically store the recovery key in:** > **The Configuration Manager database**. For more information, see [Escrow BitLocker recovery password to the site during a task sequence](/mem/configmgr/core/plan-design/changes/whats-new-in-version-2203#escrow-bitlocker-recovery-password-to-the-site-during-a-task-sequence).
>
> Stand-alone MBAM integration with Configuration Manager was only supported through Configuration Manager, version 1902. Since Configuration Manager, version 1902 is out of support, using stand-alone MBAM and the `Invoke-MbamClientDeployment.ps1` PowerShell script with currently supported versions of Configuration Manager is no longer supported. For more information, see [Versions of Configuration Manager that MBAM supports](mbam-25-supported-configurations.md#versions-of-configuration-manager-that-mbam-supports). Customers using stand-alone MBAM with Configuration Manager should [migrate to Configuration Manager BitLocker Management](/mem/configmgr/protect/deploy-use/bitlocker/migration-considerations).

This article explains how to enable BitLocker on a user's computer by using Microsoft BitLocker Administration and Monitoring (MBAM) as part of your Windows imaging and deployment process.

> [!NOTE]
> If you see a black screen at restart after the Install phase concludes indicating that the drive can't be unlocked, see [Earlier Windows versions don't start after "Setup Windows and Configuration Manager" step if Pre-Provision BitLocker is used with Windows 10, version 1511](/troubleshoot/windows-client/windows-security/earlier-versions-not-start-use-pre-provision-bitlocker).

## Prerequisites

- An existing Windows image deployment process - Microsoft Deployment Toolkit (MDT), Microsoft System Center Configuration Manager, or some other imaging tool or process - must be in place

- TPM must be enabled in the BIOS and visible to the OS

- MBAM server infrastructure must be in place and accessible

- The system partition required by BitLocker must be created

- The machine must be domain joined during imaging before MBAM fully enables BitLocker

## To enable BitLocker using MBAM 2.5 SP1 as part of a Windows deployment

### Enable BitLocker during Windows deployment with the `Invoke-MbamClientDeployment.ps1` PowerShell script

In MBAM 2.5 SP1, the recommended approach to enable BitLocker during a Windows Deployment is by using the `Invoke-MbamClientDeployment.ps1` PowerShell script.

- The `Invoke-MbamClientDeployment.ps1` script enacts BitLocker during the imaging process. When required by BitLocker policy, the MBAM agent immediately prompts the domain user to create a PIN or password when the domain user first logs on after imaging.

- Easy to use with MDT, System Center Configuration Manager, or standalone imaging processes

- Compatible with PowerShell 2.0 or higher

- Encrypt OS volume with TPM key protector

- Fully support BitLocker pre-provisioning

- Optionally encrypt FDDs

- Escrow TPM OwnerAuth
  - For Windows 7, MBAM must own the TPM for escrow to occur.
  - For Windows 8.1, Windows 10 RTM and Windows 10 version 1511, escrow of TPM OwnerAuth is supported.
  - For Windows 10, version 1607 or later, only Windows can take ownership of the TPM. When it provisions the TPM, Windows doesn't keep the TPM owner password. For more information, see [TPM owner password](/windows/security/hardware-security/tpm/change-the-tpm-owner-password).

- Escrow recovery keys and recovery key packages

- Report encryption status immediately

- New WMI providers

- Detailed logging

- Robust error handling

You can download the `Invoke-MbamClientDeployment.ps1` script from [MBAM client deployment scripts](https://www.microsoft.com/download/details.aspx?id=54439). This download is the main script that your deployment system calls to configure BitLocker drive encryption and record recovery keys with the MBAM Server.

### <a href="" id="mbam-machine-wmi-class"></a> WMI deployment methods for MBAM

To support enabling BitLocker by using the `Invoke-MbamClientDeployment.ps1` PowerShell script, MBAM 2.5 SP1 includes the following WMI methods:

#### `MBAM_Machine` WMI class

- `PrepareTpmAndEscrowOwnerAuth`: Reads the TPM OwnerAuth and sends it to the MBAM recovery database by using the MBAM recovery service. If the TPM isn't owned and autoprovisioning isn't on, it generates a TPM OwnerAuth and takes ownership. If it fails, an error code is returned for troubleshooting.

  > [!NOTE]
  > For Windows 10, version 1607 or later, only Windows can take ownership of the TPM. In addition, Windows will not retain the TPM owner password when provisioning the TPM. For more information, see [TPM owner password](/windows/security/hardware-security/tpm/change-the-tpm-owner-password).

  | Parameter | Description |
  | -------- | ----------- |
  | RecoveryServiceEndPoint | A string specifying the MBAM recovery service endpoint. |

  Here's a list of common error messages:

  | Common return values | Error message |
  | -------------------- | ------------- |
  |  **S_OK**<br />0 (0x0) | The method was successful. |
  | **MBAM_E_TPM_NOT_PRESENT**<br />2147746304 (0x80040200) | TPM isn't present in the computer or is disabled in the BIOS configuration. |
  | **MBAM_E_TPM_INCORRECT_STATE**<br />2147746305 (0x80040201) | TPM isn't in the correct state (enabled, activated, and owner installation allowed). |
  | **MBAM_E_TPM_AUTO_PROVISIONING_PENDING**<br />2147746306 (0x80040202) | MBAM can't take ownership of TPM because autoprovisioning is pending. Try again after autoprovisioning is completed. |
  | **MBAM_E_TPM_OWNERAUTH_READFAIL**<br />2147746307 (0x80040203) | MBAM can't read the TPM owner authorization value. The value might be removed after a successful escrow. On Windows 7, if others own the TPM, MBAM can't read the value. |
  | **MBAM_E_REBOOT_REQUIRED**<br />2147746308 (0x80040204) | The computer must be restarted to set TPM to the correct state. You might need to manually reboot the computer. |
  | **MBAM_E_SHUTDOWN_REQUIRED**<br />2147746309 (0x80040205) | The computer must be shut down and turned back on to set TPM to the correct state. You might need to manually reboot the computer. |
  | **WS_E_ENDPOINT_ACCESS_DENIED**<br />2151481349 (0x803D0005) | The remote endpoint denied access. |
  | **WS_E_ENDPOINT_NOT_FOUND**<br />2151481357 (0x803D000D) | The remote endpoint doesn't exist or couldn't be located. |
  | **WS_E_ENDPOINT_FAILURE<br />2151481357 (0x803D000F) | The remote endpoint couldn't process the request. |
  | **WS_E_ENDPOINT_UNREACHABLE**<br />2151481360 (0x803D0010) | The remote endpoint wasn't reachable. |
  | **WS_E_ENDPOINT_FAULT_RECEIVED**<br />2151481363 (0x803D0013) | A message containing a fault was received from the remote endpoint. Make sure you connect to the correct service endpoint. |
  | **WS_E_INVALID_ENDPOINT_URL** 2151481376 (0x803D0020) | The endpoint address URL isn't valid. The URL must start with `http` or `https`. |

- `ReportStatus`: Reads the compliance status of the volume and sends it to the MBAM compliance status database by using the MBAM status reporting service. The status includes cipher strength, protector type, protector state, and encryption state. If it fails, an error code is returned for troubleshooting.

   | Parameter | Description |
   | --------- | ----------- |
   | ReportingServiceEndPoint | A string specifying the MBAM status reporting service endpoint. |

   Here's a list of common error messages:

   | Common return values | Error message |
   | -------------------- | ------------- |
   | **S_OK**<br /> 0 (0x0) | The method was successful |
   | **WS_E_ENDPOINT_ACCESS_DENIED**<br />2151481349 (0x803D0005) | The remote endpoint denied access. |
   | **WS_E_ENDPOINT_NOT_FOUND**<br />2151481357 (0x803D000D) | The remote endpoint doesn't exist or couldn't be located. |
   | **WS_E_ENDPOINT_FAILURE**<br /> 2151481357 (0x803D000F) | The remote endpoint couldn't process the request. |
   | **WS_E_ENDPOINT_UNREACHABLE**<br />2151481360 (0x803D0010) | The remote endpoint wasn't reachable. |
   | **WS_E_ENDPOINT_FAULT_RECEIVED**<br />2151481363 (0x803D0013) | A message containing a fault was received from the remote endpoint. Make sure you connect to the correct service endpoint. |
   | **WS_E_INVALID_ENDPOINT_URL**<br />2151481376 (0x803D0020) | The endpoint address URL isn't valid. The URL must start with `http` or `https`. |

#### `MBAM_Volume` WMI class

- `EscrowRecoveryKey`: Reads the recovery numerical password and key package of the volume and sends them to the MBAM recovery database by using the MBAM recovery service. If it fails, an error code is returned for troubleshooting.

   | Parameter | Description |
   | --------- | ----------- |
   | RecoveryServiceEndPoint | A string specifying the MBAM recovery service endpoint. |

   Here's a list of common error messages:

   | Common return values | Error message |
   | -------------------- | ------------- |
   | **S_OK**<br />0 (0x0) | The method was successful |
   | **FVE_E_LOCKED_VOLUME**<br />2150694912 (0x80310000) | The volume is locked. |
   | **FVE_E_PROTECTOR_NOT_FOUND**<br />2150694963 (0x80310033) | A numerical password protector wasn't found for the volume. |
   | **WS_E_ENDPOINT_ACCESS_DENIED**<br />2151481349 (0x803D0005) | The remote endpoint denied access. |
   | **WS_E_ENDPOINT_NOT_FOUND**<br />2151481357 (0x803D000D) | The remote endpoint doesn't exist or couldn't be located. |
   | **WS_E_ENDPOINT_FAILURE**<br />2151481357 (0x803D000F) | The remote endpoint couldn't process the request. |
   | **WS_E_ENDPOINT_UNREACHABLE**<br />2151481360 (0x803D0010) | The remote endpoint wasn't reachable. |
   | **WS_E_ENDPOINT_FAULT_RECEIVED**<br />2151481363 (0x803D0013) | A message containing a fault was received from the remote endpoint. Make sure you connect to the correct service endpoint. |
   | **WS_E_INVALID_ENDPOINT_URL**<br />2151481376 (0x803D0020) | The endpoint address URL isn't valid. The URL must start with `http` or `https`. |

### Deploy MBAM by using Microsoft Deployment Toolkit (MDT) and PowerShell

1.  In MDT, create a new deployment share or open an existing deployment share.

    > [!NOTE]
    > You can use the `Invoke-MbamClientDeployment.ps1` PowerShell script with any imaging process or tool. This section shows how to integrate it by using MDT, but the steps are similar to integrating it with any other process or tool.

    > [!CAUTION]
    > If you use BitLocker preprovisioning in Windows PE, and want to maintain the TPM owner authorization value, you must add the `SaveWinPETpmOwnerAuth.wsf` script in Windows PE immediately before the installation restarts into the full OS. **If you don't use this script, you'll lose the TPM owner authorization value on restart.**

2.  Copy `Invoke-MbamClientDeployment.ps1` to `<DeploymentShare>\Scripts`. If you're using pre-provisioning, copy the `SaveWinPETpmOwnerAuth.wsf` file into `<DeploymentShare>\Scripts`.

3.  Add the MBAM 2.5 SP1 client application to the Applications node in the deployment share.

    1.  Under the **Applications** node, select **New Application**.
    2.  Select **Application with Source Files**. Select **Next**.
    3.  In **Application Name**, type "MBAM 2.5 SP1 Client". Select **Next**.
    4.  Browse to the directory containing `MBAMClientSetup-<Version>.msi`. Select **Next**.
    5.  Type "MBAM 2.5 SP1 Client" as the directory to create. Select **Next**.
    6.  Enter `msiexec /i MBAMClientSetup-<Version>.msi /quiet` at the command line. Select **Next**.
    7.  Accept the remaining defaults to complete the New Application wizard.

4.  In MDT, right-click the name of the deployment share and select **Properties**. Select the **Rules** tab. Add the following lines:

    `SkipBitLocker=YES``BDEInstall=TPM``BDEInstallSuppress=NO``BDEWaitForEncryption=YES`

    Select OK to close the window.

5.  Under the Task Sequences node, edit an existing task sequence used for Windows Deployment. If you want, you can create a new task sequence by right-clicking the **Task Sequences** node, selecting **New Task Sequence**, and completing the wizard.

    On the **Task Sequence** tab of the selected task sequence, do these steps:

    1.  Under the **Preinstall** folder, enable the optional task **Enable BitLocker (Offline)** if you want BitLocker enabled in WinPE, which encrypts used space only.
    2.  To persist TPM OwnerAuth when using pre-provisioning, allowing MBAM to escrow it later, do the following:

        1.  Find the **Install Operating System** step
        2.  Add a new **Run Command Line** step after it
        3.  Name the step **Persist TPM OwnerAuth**
        4.  Set the command line to `cscript.exe "%SCRIPTROOT%/SaveWinPETpmOwnerAuth.wsf"`

            > [!NOTE]
            > For Windows 10, version 1607 or later, only Windows can take ownership of the TPM. When provisioning the TPM, Windows doesn't keep the TPM owner password. For more information, see [TPM owner password](/windows/security/hardware-security/tpm/change-the-tpm-owner-password).

    3.  In the **State Restore** folder, delete the **Enable BitLocker** task.
    4.  In the **State Restore** folder under **Custom Tasks**, create a new **Install Application** task and name it **Install MBAM Agent**. Select the **Install Single Application** radio button and browse to the MBAM 2.5 SP1 client application created earlier.
    5.  In the **State Restore** folder under **Custom Tasks**, create a new **Run PowerShell Script** task (after the MBAM 2.5 SP1 Client application step) with the following settings (update the parameters as appropriate for your environment):

        - Name: Configure BitLocker for MBAM
        - PowerShell script: `Invoke-MbamClientDeployment.ps1`
        - Parameters:

            | Parameter | Requirement | Description |
            |--|--|--|
            | `-RecoveryServiceEndpoint` | Required | MBAM recovery service endpoint. |
            | `-StatusReportingServiceEndpoint` | Optional | MBAM status reporting service endpoint. |
            | `-EncryptionMethod` | Optional | Encryption method (default: AES 128). |
            | `-EncryptAndEscrowDataVolume` | Switch | Specify to encrypt data volumes and escrow data volume recovery keys. |
            | `-WaitForEncryptionToComplete` | Switch | Specify to wait for the encryption to complete. |
            | `-DoNotResumeSuspendedEncryption` | Switch | Specify that the deployment script won't resume suspended encryption. |
            | `-IgnoreEscrowOwnerAuthFailure` | Switch | Specify to ignore TPM owner-auth escrow failure. It should be used in scenarios where MBAM isn't able to read the TPM owner-auth. For example, if TPM auto provisioning is enabled. |
            | `-IgnoreEscrowRecoveryKeyFailure` | Switch | Specify to ignore volume recovery key escrow failure. |
            | `-IgnoreReportStatusFailure` | Switch | Specify to ignore status reporting failure. |

## To enable BitLocker using MBAM 2.5 or earlier as part of a Windows deployment

1.  Install the MBAM client. For instructions, see [How to deploy the MBAM client by using a command line](how-to-deploy-the-mbam-client-by-using-a-command-line.md).

2.  Join the computer to a domain (recommended).

    - If the computer isn't joined to a domain, the recovery password isn't stored in the MBAM Key Recovery service. By default, MBAM doesn't allow encryption to occur unless the recovery key can be stored.

    - If a computer starts in recovery mode before the recovery key is stored on the MBAM Server, no recovery method is available, and the computer has to be reimaged.

3.  Open a command prompt as an administrator, and stop the MBAM service.

4.  Set the service to **Manual** or **On demand** by typing the following commands:

    `net stop mbamagent`

    `sc config mbamagent start= demand`

5.  Set the registry values so that the MBAM client ignores the group policy settings and instead sets encryption to start the time Windows is deployed to that client computer.

    > [!CAUTION]
    > This step describes how to modify the Windows registry. Using Registry Editor incorrectly can cause serious issues that can require you to reinstall Windows. We can't guarantee that issues resulting from the incorrect use of Registry Editor can be resolved. Use Registry Editor at your own risk.

    1.  Set the TPM for **Operating system only encryption**, run Regedit.exe, and then import the registry key template from `C:\Program Files\Microsoft\MDOP MBAM\MBAMDeploymentKeyTemplate.reg`.

    2.  In Regedit.exe, go to `HKLM\SOFTWARE\Microsoft\MBAM`, and configure the settings that are listed in the following table.

        > [!NOTE]
        > You can set group policy settings or registry values related to MBAM here. These settings override previously set values.

        | Registry entry | Configuration settings |
        |---|---|
        | DeploymentTime | 0 = Off<br> 1 = Use deployment time policy settings (default) - use this setting to enable encryption at the time Windows is deployed to the client computer. |
        | UseKeyRecoveryService | 0 = Don't use key escrow. The next two registry entries aren't required in this case.<br> 1 = Use key escrow in Key Recovery system (default) <br> This setting is recommended, which enables MBAM to store the recovery keys. The computer must be able to communicate with the MBAM Key Recovery service. Verify that the computer can communicate with the service before you proceed. |
        | KeyRecoveryOptions | 0 = Uploads Recovery Key only<br>1 = Uploads Recovery Key and Key Recovery Package (default) |
        | KeyRecoveryServiceEndPoint | Set this value to the URL for the server running the Key Recovery service, for example, `https://<computer name>/MBAMRecoveryAndHardwareService/CoreService.svc`. |

6.  The MBAM client restarts the system during the MBAM client deployment. When you're ready for this restart, run the following command at a command prompt as an administrator:

    `net start mbamagent`

7.  When the computers restarts, and the BIOS prompts you, accept the TPM change.

8.  During the Windows client operating system imaging process, when you're ready to start encryption, open a command prompt as an administrator, and type the following commands to set the start to **Automatic** and to restart the MBAM client agent:

    `sc config mbamagent start= auto`

    `net start mbamagent`

9.  To delete the bypass registry values, run Regedit.exe, and go to the `HKLM\SOFTWARE\Microsoft` registry entry. Right-click the **MBAM** node, and then select **Delete**.

## Related articles

[Deploying the MBAM 2.5 client](deploying-the-mbam-25-client.md)

[Planning for MBAM 2.5 client deployment](planning-for-mbam-25-client-deployment.md)
