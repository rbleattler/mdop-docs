---
title: Deploy the App-V Client
description: Describes How to Deploy the App-V Client
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.date: 11/05/2018
---

# Deploy the App-V client

Use the following procedure to install the Microsoft Application Virtualization (App-V) 5.0 client and Remote Desktop Services client. You must install the version of the client that matches the operating system of the target computer.

## What to do before you start

### Review and install the software prerequisites

Install the prerequisite software that corresponds to the version of App-V that you're installing:

- [About App-V 5.0 SP3](about-app-v-50-sp3.md)

- App-V 5.0 SP1 and App-V 5.0 SP2: no new prerequisites in these versions.

- [App-V 5.0 Prerequisites](app-v-50-prerequisites.md)

### Review the client coexistence and unsupported scenarios, as applicable to your installation

For deploying coexisting App-V clients, see [Planning for the App-V 5.0 Sequencer and Client Deployment](planning-for-the-app-v-50-sequencer-and-client-deployment.md).

For unsupported or limited installation scenarios, see [App-V 5.0 Supported Configurations](app-v-50-supported-configurations.md).

### Review the locations for client registry, log, and troubleshooting information

#### Client registry information

By default, after you install the App-V 5.0 client, the client information is stored in the registry in the following registry key: `HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\APPV\CLIENT`

When you deploy a virtualized package to a computer that is running the App-V client, the associated package data is stored in the following location: `C:\ProgramData\App-V`

However, you can reconfigure this location with the following registry key: `HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\APPV\CLIENT\STREAMING\PACKAGEINSTALLATIONROOT`

#### Client log files

For log file information that's associated with the App-V 5.0 client, search in the following log: `Event logs / Applications and Services Logs / Microsoft / AppV`

In App-V 5.0 SP3, some logs are consolidated and moved to the following location: `Event logs / Applications and Services Logs / Microsoft / AppV / ServiceLog`

For a list of the moved logs, see [About App-V 5.0 SP3](about-app-v-50-sp3.md#bkmk-event-logs-moved).

Packages that are currently stored on computers that run the App-V 5.0 Client are saved to the following location: `C:\ProgramData\App-V\<package id>\<version id>`

#### Client installation troubleshooting information

See the error log in the `%temp%` folder. To review the log files, select `Start`, type `%temp%`, and then look for the `appv_log`.

## To install the App-V 5.0 Client

1. Copy the App-V 5.0 client installation file to the computer on which it will be installed.<p><p>Choose from the following client types:

    | Client type | File to use |
    |--|--|
    | Standard version of the client | **appv_client_setup.exe** |
    | Remote Desktop Services version of the client | **appv_client_setup_rds.exe** |

2. Open the installation file, and select **Install**. Before the installation begins, the installer checks the computer for any missing [App-V 5.0 Prerequisites](app-v-50-prerequisites.md).

3. Review and accept the Software License Terms, choose whether to use Microsoft Update and whether to participate in the Microsoft Customer Experience Improvement Program, and select **Install**.

4. On the **Setup completed successfully** page, select **Close**.

   The installation creates the following entries for the App-V client in **Programs**:

    - `.exe`

    - `.msi`

    - `language pack`

   > [!NOTE]
   > After the installation, only the .exe file can be uninstalled.

## To install the App-V 5.0 client using a script

1. Install all of the required prerequisite software on the target computers. For more information, see [What to do before you start](#what-to-do-before-you-start). If you install the client by using an .msi file, the installation fails if any prerequisites are missing.

2. To use a script to install the App-V 5.0 client, use the following parameters with `appv_client_setup.exe`.

   > [!NOTE]
   > The client Windows Installer (.msi) supports the same set of switches, except for the `/LOG` parameter.

| Parameter | Description | Example usage |
|--|--|--|
| `/INSTALLDIR` | Specifies the installation directory. | `/INSTALLDIR=C:\Program Files\AppV Client` |
| `/CEIPOPTIN` | Enables participation in the Customer Experience Improvement Program. | `/CEIPOPTIN=[0 | 1]` |
| `/MUOPTIN` | Enables Microsoft Update. | `/MUOPTIN=[0 | 1]` |
| `/PACKAGEINSTALLATIONROOT` | Specifies the directory in which to install all new applications and updates. | `/PACKAGEINSTALLATIONROOT='C:\App-V Packages'` |
| `/PACKAGESOURCEROOT` | Overrides the source location for downloading package content. | `/PACKAGESOURCEROOT='https://packageStore'` |
| `/AUTOLOAD` | Specifies how new packages will be loaded by App-V 5.0 on a specific computer. The following options are enabled: [`1`]; automatically load all packages [`2`]; or automatically load no packages [`0`]. | `/AUTOLOAD=[0 | 1 | 2]` |
| `/SHAREDCONTENTSTOREMODE` | Specifies that streamed package contents won't be saved to the local hard disk. | `/SHAREDCONTENTSTOREMODE=[0 | 1]` |
| `/MIGRATIONMODE` | Allows the App-V 5.0 client to modify the shortcuts and FTAs associated with the packages created with a previous version. | `/MIGRATIONMODE=[0 | 1]` |
| `/ENABLEPACKAGESCRIPTS` | Enables the scripts defined in the package manifest file or configuration files that should run. | `/ENABLEPACKAGESCRIPTS=[0 | 1]` |
| `/ROAMINGREGISTRYEXCLUSIONS` | Specifies the registry paths that won't roam with a user profile. | `/ROAMINGREGISTRYEXCLUSIONS=software\classes;software\clients` |
| `/ROAMINGFILEEXCLUSIONS` | Specifies the file paths relative to %userprofile% that don't roam with a user's profile. | `/ROAMINGFILEEXCLUSIONS 'desktop;my pictures'` |
| `/S[1-5]PUBLISHINGSERVERNAME` | Displays the name of the publishing server. | `/S2PUBLISHINGSERVERNAME=MyPublishingServer` |
| `/S[1-5]PUBLISHINGSERVERURL` | Displays the URL of the publishing server. | `/S2PUBLISHINGSERVERURL=\pubserver` |
| `/S[1-5]GLOBALREFRESHENABLED` | Enables a global publishing refresh. | `/S2GLOBALREFRESHENABLED=[0 | 1]` |
| `/S[1-5]GLOBALREFRESHONLOGON` | Initiates a global publishing refresh when a user logs on. | `/S2LOGONREFRESH=[0 | 1]` |
| `/S[1-5]GLOBALREFRESHINTERVAL` | Specifies the publishing refresh interval, where `0` indicates don't periodically refresh. | `/S2PERIODICREFRESHINTERVAL=[0-744]` |
| `/S[1-5]GLOBALREFRESHINTERVALUNIT` | Specifies the interval unit (Hours[0], Days[1]). | `/S2GLOBALREFRESHINTERVALUNIT=[0 | 1]` |
| `/S[1-5]USERREFRESHENABLED` | Enables user publishing refresh. | `/S2USERREFRESHENABLED=[0 | 1]` |
| `/S[1-5]USERREFRESHONLOGON` | Initiates a user publishing refresh when a user logs on. | `/S2LOGONREFRESH=[0 | 1]` |
| `/S[1-5]USERREFRESHINTERVAL` | Specifies the publishing refresh interval, where `0` indicates don't periodically refresh. | `/S2PERIODICREFRESHINTERVAL=[0-744]` |
| `/S[1-5]USERREFRESHINTERVALUNIT` | Specifies the interval unit (Hours[0], Days[1]). | `/S2USERREFRESHINTERVALUNIT=[0 | 1]` |
| `/Log` | Specifies a location where the log information is saved. | `/log C:\logs\log.log` |
| `/q` | Specifies an unattended installation. | `/q` |
| `/REPAIR` | Repairs a previous client installation. | `/REPAIR` |
| `/NORESTART` | Prevents the computer from rebooting after the client installation. The parameter prevents the end-user computer from rebooting after each update is installed and lets you schedule the reboot at your convenience. For example, you can install App-V 5.0 SPX and then install Hotfix Package Y without rebooting after the Service Pack installation. After the installation, you must reboot before you start using App-V. | `/NORESTART` |
| `/UNINSTALL` | Uninstalls the client. | `/UNINSTALL` |
| `/ACCEPTEULA` | Accepts the license agreement. This is required for an unattended installation. | `/ACCEPTEULA` or `/ACCEPTEULA=1` |
| `/LAYOUT` | Specifies the associated layout action. It also extracts the Windows Installer (.msi) and script files to a folder without installing App-V 5.0. No value is expected. | `/LAYOUT` |
| `/LAYOUTDIR` | Specifies the layout directory. Requires a string value. | `/LAYOUTDIR="C:\Application Virtualization Client"` |
| `/?, /h, /help` | Requests help about the previous installation parameters. | `/?, /h, /help` |

## To install the App-V 5.0 client by using the Windows Installer (.msi) file

1. Install the required prerequisites on the target computers. For more information, see [What to do before you start](#what-to-do-before-you-start). If any prerequisites aren't met, the installation fails.

2. Make sure that the target computers don't have any pending restarts before you install the client using the App-V 5.0 Windows Installer (.msi) files. The Windows Installer files don't flag a pending restart.

3. Deploy one of the following Windows Installer files to the target computer. The file that you specify must match the configuration of the target computer.

    | Type of deployment                                          | Deploy this file          |
    |------------------------------------------------------------|---------------------------|
    | Computer is running a 32-bit Microsoft Windows operating system | `appv_client_MSI_x86.msi` |
    | Computer is running a 64-bit Microsoft Windows operating system | `appv_client_MSI_x64.msi` |
    | You're deploying the App-V 5.0 Remote Desktop Services client | `appv_client_rds_MSI_x64.msi` |

4. Using the information in the following table, select the appropriate language pack **.msi** to install, based on the desired language for the target computer. The **xxxx** in the table refers to the target locale of the language pack.

    - The language packs are common to both the standard App-V 5.0 client and the Remote Desktop Services version of the App-V 5.0 client.

    - If you install the App-V 5.0 client using the **.exe**, the installer deploys only the language pack that matches the operating system running on the target computer.

    - To deploy more language packs on a target computer, use the procedure **To install the App-V 5.0 client by using Windows Installer (.msi) file**.

    | Type of deployment                                          | Deploy this file           |
    |------------------------------------------------------------|----------------------------|
    | Computer is running a 32-bit Microsoft Windows operating system | `appv_client_LP_xxxx_ x86.msi` |
    | Computer is running a 64-bit Microsoft Windows operating system | `appv_client_LP_xxxx_ x64.msi` |

## Related information

[Deploying App-V 5.0](deploying-app-v-50.md)

[About Client Configuration Settings](about-client-configuration-settings.md)

[How to Uninstall the App-V 5.0 Client](how-to-uninstall-the-app-v-50-client.md)
