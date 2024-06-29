---
title: Microsoft Application Virtualization Management System Release Notes 4.5 SP1
description: Microsoft Application Virtualization Management System Release Notes 4.5 SP1
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.date: 08/30/2016
---


# Microsoft Application Virtualization Management System Release Notes 4.5 SP1

> [!IMPORTANT]
> Read these Release Notes thoroughly before you install the Application Virtualization Management System. These Release Notes contain information that you need to successfully install the Application Virtualization Management System. These Release Notes contain information that isn't available in the product documentation. If there's a discrepancy between these Release Notes and other Application Virtualization Management System documentation, the latest change should be considered authoritative.

## About Microsoft Application Virtualization 4.5 Service Pack 1


These Release Notes have been updated to reflect the changes introduced with Microsoft Application Virtualization (App-V) 4.5 Service Pack 1 (SP1). This service pack contains the following changes:

-   Support for Windows 7 and Windows Server 2008 R2: App-V 4.5 SP1 provides support for Windows 7 and Windows Server 2008 R2, including support for Windows 7 features such as the taskbar, AppLocker, BranchCache, and BitLocker To Go.  Windows Server 2008 R2 support is for the Application Virtualization Server only.

-   Support for third-party Kerberos realms: App-V 4.5 SP1 provides support for environments that have a trust relationship and mapped user accounts between a Windows domain and an MIT Kerberos realm, which is a scenario that is common at many universities. For information on how to enable this support, [How to Configure the Client for MIT Kerberos Realm Support](how-to-configure-the-client-for-mit-kerberos-realm-support.md).

-   Improved support for application publishing and streaming via HTTP/HTTPS: App-V 4.5 SP1 provides support for application publishing and streaming via the HTTP/HTTPS protocols for Windows XP Home Edition, Windows Vista Home Basic, and Windows 7 Home Basic.

-   Customer Feedback and Hotfix Rollup: App-V 4.5 SP1 also includes a rollup up of fixes to address issues found since the Microsoft Application Virtualization (App-V) 4.5 CU1 release. The updates are a result of a combination of known issues and customer feedback from our internal teams, partners, and customers who are using App-V 4.5.

## Protect Against Security Vulnerabilities and Viruses

To help protect against security vulnerabilities and viruses, we recommend that you install the latest available security updates for any new software being installed.

## Known Issues with Application Virtualization 4.5 SP1


This section provides the most up-to-date information about issues with Microsoft Application Virtualization (App-V) 4.5 SP1. These issues don't appear in the product documentation and in some cases might contradict existing product documentation.

### Guidance for installing Server Management Console

If you need to install management software onto systems other than the primary Application Virtualization publishing and streaming server, the server install supports installing the Management Console and Management Web service on separate servers from the primary App-V Management Server. To distribute the management components across multiple servers, Kerberos delegation must be enabled on the server where the Web service is installed. For information on how to enable this support, see [How to Configure the Server to be Trusted for Delegation](how-to-configure-the-server-to-be-trusted-for-delegation.md).

### Guidance for installing or upgrading clients to App-V 4.5 SP1 using setup.msi

When installing or upgrading your App-V clients to App-V 4.5 SP1 by using setup.msi, the prerequisites aren't installed automatically.

WORKAROUND   You must manually install the prerequisites before installing or upgrading the App-V client to App-V 4.5 SP1. For detailed procedures for installing the prerequisites and the App-V client, see [How to Install the Client by Using the Command Line](how-to-install-the-client-by-using-the-command-line-new.md).

When this has been completed, install the App-V 4.5 SP1 client by using setup.msi with elevated privileges. This file is available on the App-V 4.5 SP1 release media in the Installers\\Client folder.

When installing Microsoft Application Error Reporting, use the following command if you're installing or upgrading to the App-V 4.5 SP1 Desktop client:

`msiexec /i dw20shared.msi APPGUID={93468B43-C19D-44F9-8BCC-114076DB0443}  allusers=1 reboot=suppress REINSTALL=all REINSTALLMODE=vomus`

Alternatively, if you're installing or upgrading to the App-V 4.5 SP1 Client for Remote Desktop Services (formerly Terminal Services), use the following command:

`msiexec /i dw20shared.msi APPGUID={0042AD3C-99A4-4E58-B5F0-744D5AD96E1C} allusers=1 reboot=suppress REINSTALL=all REINSTALLMODE=vomus`

> [!NOTE]
> The APPGUID parameter references the product code of the App-V client that you install or upgrade. The product code is unique for each setup.msi. You can use the Orca database editor or a similar tool to examine Windows Installer files and determine the product code. This step is required for all installations or upgrades to App-V 4.5 SP1.



### Improving performance when sequencing the .NET Framework

When sequencing the .NET Framework, you might experience reduced system performance because the Microsoft .NET Framework NGEN service attempts to precompile assemblies as a background task.

WORKAROUND   When sequencing the .NET Framework, disable the Microsoft .NET Framework NGEN service (mscorsvw.exe) after completing the monitoring phase. You must use the **Virtual Services** tab in the Sequencer and change the startup type to disabled.

### When you uninstall the Microsoft Application Virtualization Client, user settings associated with the user performing the uninstall will be deleted

When you uninstall the App-V Client, the Windows Installer will remove Application Virtualization settings from the current user's profile. If your computer uses roaming profiles, don't use your personal network account to uninstall the client because it removes settings for your virtual applications on all of your computers.

WORKAROUND   You should perform the App-V Client uninstall with an administrative account that isn't used for running virtual applications.

### Edits made on the virtual file system and virtual registry tabs must be saved while running the Sequencing wizard

If you open a package to perform an upgrade, or if you have already run the Sequencing wizard with a new package and make changes to the package in the virtual file system or virtual registry tabs, those changes aren't automatically saved.

WORKAROUND   Save the changes before rerunning the wizard, to ensure that they're reflected inside the wizard's virtual environment.

### Command-line Sequencer must be run from an elevated command prompt

When you use the command-line Sequencer, it doesn't prompt for elevation.

WORKAROUND   Run the command-line Sequencer using an elevated command prompt.

### Short path variable names in OSD files can cause errors

If you receive error 450478-1F702339-0000010B "The directory name is invalid" when starting a virtual application on the client, it's possible that the variable in the OSD is set incorrectly. This can happen if the application's installer sets a short path name during sequencing.

WORKAROUND   Remove the trailing tilde from any CSIDL variable that exists in the OSD file.

### <a name="correct-syntax-for-decodepath-parameter-for-command-line-sequencer-"></a>Correct syntax for DECODEPATH parameter for command-line Sequencer

In the command-line Sequencer, when opening a package for upgrade and decoding it to the root of the Q drive, the syntax for the *DECODEPATH* parameter shouldn't include a trailing slash.

WORKAROUND   You can use **Q:** rather than **Q:\\** (omitting the trailing "\\" character).

### <a name="when-upgrading-4-2-packages--you-encounter-problems-caused-by-windows-installer-files-in-the-virtual-file-system-"></a>When upgrading 4.2 packages, you encounter problems caused by Windows Installer files in the Virtual File System

When upgrading a package from 4.2, you might experience issues relating to a mismatch of Windows Installer system files that were included by default in 4.2 and the Windows Installer libraries locally installed on your Sequencing workstation. The following files are located in CSIDL\_SYSTEM\\:

- cabinet.dll

- msi.dll

- msiexec.exe

- msihnd.dll

- msimsg.dll

WORKAROUND   Delete all of the preceding files from the package. Delete the mappings on the **VFS** tab and the actual files in the CSIDL\_SYSTEM folder in your decode path.

### <a name="on-windows-xp--client-install-logging-is-not-enabled-by-default-"></a>On Windows XP, client install logging isn't enabled by default

When installing the client, to ensure that any install errors are captured for troubleshooting purposes, you should enable logging by using the command line.

WORKAROUND   Add the parameter `/l*vx! log.txt` to the command line, as shown in the following example:

```cmd
setup.exe /s /v"/qn /l*vx! log.txt"

msiexec.exe /i setup.msi /qn /l*vx! log.txt
```

Alternatively, you can set the registry key to the following value:

`[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Installer] "Logging"="voicewarmupx!"`

### For Kerberos authentication to work, Service Principal Names (SPNs) must be registered for IIS

When using IIS 6.0 or 7.0 for icon or OSD file retrieval and streaming of packages, for Kerberos authentication to be enabled, the SPNs must be registered as follows:

-   On the IIS server, run the following commands by using the SETSPN.EXE Resource Kit tool. The server fully qualified domain name (FQDN) must be used.

    `Setspn -r SOFTGRID/<Server FQDN>`

    `Setspn -r HTTP/<Server FQDN>`

### .NET compatibility changes

Microsoft Application Virtualization (App-V) Cumulative Update 1 or later supports sequencing the .NET Framework on Windows XP (SP2 or later). Sequencing routines for .NET applications that were written for SoftGrid 4.2 might need to be updated when used with the App-V 4.5 Sequencer.

### <a name="after-client-upgrade-from-app-v-4-2--some-applications-are-not-shown-"></a>After client upgrade from App-V 4.2, some applications aren't shown

Check for the following error in the log: "The Application Virtualization Client couldn't parse the OSD file". The App-V 4.5 client filters out applications that have an OSD file containing an empty OS tag (&lt;OS&gt;&lt;/OS&gt;).

WORKAROUND   Delete the empty OS tag from the OSD file.

### The App-V server requires exemptions in its firewall for certain processes

For the server to stream applications correctly, the server's core processes, including the dispatcher, need access through the firewall.

WORKAROUND   Set exemptions in the server's firewall for the following processes: sghwsvr.exe and sghwdsptr.exe. This applies to the App-V Management Server and App-V Streaming Server.

### When the server installer is run in silent mode, it doesn't correctly check for MSXML6

The App-V Management Server depends on MSXML6. However, if you run the installer in silent mode—for example, by using the command "msiexec -i setup.msi /qn" on a system where MSXML6 isn't already installed—the installer doesn't detect the missing dependency and installs anyway. Therefore, when clients attempt to refresh publishing information from the App-V Management Server, they'll see failures.

WORKAROUND   Verify that MSXML6 is installed on the system before attempting a silent install of the App-V Management Server.

### Error code 000C800 when attempting to connect to the Application Virtualization Management Console

An Application Virtualization administrator who isn't a local administrator on the App-V Management Web Service server receives an error (Error code: 000C800) when attempting to connect to the App-V Management Console, and the sftmmc.log entry will indicate that access to SftMgmt.udl is denied. To successfully connect to the App-V Management Console, an administrator who doesn't have local administrator rights on the App-V Management Web Service server must have at least read and execute permissions to the SftMgmt.udl file.

The Application Virtualization administrators must be given read and execute permissions to the SftMgmt.UDL file under `%systemdrive%\Program Files\Microsoft System Center App Virt Management Server\App Virt Management Service`.

### Client installer command-line parameters are ignored when used with KEEPCURRENTSETTINGS=1

When used with `KEEPCURRENTSETTINGS=1`, the following client installer command-line parameters are ignored: `SWICACHESIZE`, `MINFREESPACEMB`, `ALLOWINDEPENDENTFILESTREAMING`, `APPLICATIONSOURCEROOT`, `ICONSOURCEROOT`, `OSDSOURCEROOT`, `SYSTEMEVENTLOGLEVEL`, `SWIGLOBALDATA`, `DOTIMEOUTMINUTES`, `SWIFSDRIVE`, `AUTOLOADTARGET`, `AUTOLOADTRIGGERS`, `SWIUSERDATA`, and `REQUIRESECURECONNECTION`.

WORKAROUND   If you have settings you want to retain, use `KEEPCURRENTSETTINGS=1` and then set the other parameters after deployment. The App-V ADM Template can be used to set the following client settings: `APPLICATIONSOURCEROOT`, `ICONSOURCEROOT`, `OSDSOURCEROOT`, `AUTOLOADTARGET`, `AUTOLOADTRIGGERS`, `DOTIMEOUTMINUTES`, and `ALLOWINDEPENDENTFILESTREAMING`.
