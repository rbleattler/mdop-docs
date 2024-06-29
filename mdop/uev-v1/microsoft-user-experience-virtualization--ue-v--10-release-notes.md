---
title: Microsoft User Experience Virtualization (UE-V) 1.0 Release Notes
description: Microsoft User Experience Virtualization (UE-V) 1.0 Release Notes
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.date: 08/30/2016
---

# Microsoft User Experience Virtualization (UE-V) 1.0 Release Notes

You should read these release notes thoroughly before you install UE-V. The release notes contain information that is required to successfully install User Experience Virtualization, and contain additional information that isn't available in the product documentation. If there are differences between these release notes and other UE-V documentation, the latest change should be considered authoritative. These release notes supersede the content that is included with this product.

## UE-V known issues

This section contains release notes for User Experience Virtualization.

### Registry settings fail to synchronize between App-V and native applications on the same computer

When a computer has an application that is available through both the Application Virtualization (App-V) application and a native installation application (installed with an .msi file), the registry-based settings don't synchronize between the technologies.

WORKAROUND: To resolve this problem, run the application by selecting one of the two technologies, but not both.

### Windows 8 setting synchronization fails with error: "boost::filesystem::exists::Incorrect user name or password"

The Windows® 8 operating system settings synchronization fails with the following error message: **boost::filesystem::exists::Incorrect user name or password**. To check for operational log events, open the **Event Viewer** and navigate to **Applications and Services Logs** / **Microsoft** / **User Experience Virtualization** / **Logging** / **Operational**. Network shares that are used for UE-V settings storage locations should reside in the same Active Directory domain as the user. Otherwise, the following error might occur: "Incorrect user name or password".

WORKAROUND: Use network shares from the same Active Directory domain as the user.

### Email signature roaming for Outlook 2010

UE-V roams the Outlook 2010 signature files between devices. However, the default signature options for new messages and replies/forwards aren't. These two settings are stored in the Outlook profile, which UE-V doesn't roam.

WORKAROUND: None.

### Synchronization settings don't synchronize on expected interval when running in slow-link mode

Under normal conditions, settings storage locations should be available over a fast link network connection. In slow-link mode, synchronization will only occur on a periodic basis. By default, the slow-link mode synchronization schedule is set to every 360 minutes.

WORKAROUND: To change the frequency of the background synchronization for computers in slow-link mode, you can configure the Group Policy for Background Sync policy for **Offline files**.

### Special characters don't synchronize

Certain characters, such as currency symbols, don't synchronize between Windows 7 and Windows 8 computers that run the UE-V agent.

WORKAROUND: None.

### UE-V doesn't support roaming settings between 32-bit and 64-bit versions of Microsoft Office

We recommend that you install the 32-bit version of Microsoft Office for both 32-bit and 64-bit operating systems. To choose the Microsoft Office version that you need, see [Choose between the 64-bit or 32-bit version of Office](https://support.microsoft.com/office/choose-between-the-64-bit-or-32-bit-version-of-office-2dee7807-8f95-4d0c-b5fe-6c6f49b8d261). UE-V supports roaming settings between identical architecture versions of Office. For example, 32-bit Office settings will roam between all 32-bit Office instances. UE-V doesn't support roaming settings between 32-bit and 64-bit versions of Office.

WORKAROUND: None

### Other folders on the share with the setting storage location are unavailable in slow-connection mode

Settings store shares shouldn't be located on a network share that is used for other folders that must always be available. When the network share that hosts the setting storage location goes into slow-connection mode, the only available folder is the settings storage location folder. Other folders on the Share aren't available in slow-connection mode.

Workaround: None

### Favicons that are associated with Internet Explorer 9 favorites don't roam

The favicons that are associated with Internet Explorer 9 favorites aren't roamed by User Experience Virtualization and don't appear when the favorites first appear on a new computer.

WORKAROUND: Favicons appear with their associated favorites once the bookmark is used and cached in the Internet Explorer 9 browser.

### File settings paths are stored in registry

Some application settings store the paths of their configuration and settings files as values in the registry. The files that are referenced as paths in the registry must be synchronized when settings are roamed between computers.

WORKAROUND: Use folder redirection or some other technology to ensure that any files that are referenced as file settings paths are present and placed in the same location on all computers where settings roam.

### Paths longer than 260 characters aren't supported

Settings storage paths that are longer than 260 characters aren't supported. Copying the UE-V settings packages to settings storage paths that are longer than 260 characters will fail and generate the following exception message in the UE-V operational event log: **\[boost::filesystem::copy\_file: The system cannot find the path specified\]**. To check for operational log events, open the **Event Viewer** and navigate to **Applications and Services Logs** / **Microsoft** / **User Experience Virtualization** / **Logging** / **Operational**.

File settings paths that are longer than 260 characters aren't currently supported. File settings that are referenced in UE-V settings location templates can't be located in a directory path that is longer than 260 characters.

WORKAROUND: None.

### UE-V agent delays upon sign out or sign in

If a sign in or sign out occurs before Offline Files has determined that a slow link is in place, sign out or sign in might be delayed. The Offline Files feature may take up to three minutes to detect the current network state. If the sign in or shutdown occurs before Offline Files has determined that the computer is connected to a slow link, the UE-V settings package is sent to the server instead of the local cache.

WORKAROUND: None.

### Settings conflict when trying to roam operating system settings on Windows 8

On Windows 8 if Microsoft Account Sync is enabled along with UE-V for operating system settings, the settings that are applied may be inconsistent.

WORKAROUND: Do one of the following:

-   Disable Microsoft Account Sync if you're using UE-V to roam operating system settings

-   Disable UE-V for operating system settings

### Some operating system settings only roam between like operating system versions

Operating system settings for Narrator and currency characters specific to the locale will only roam across like operating system versions of Windows. For example currency characters will only roam from Windows 7 to Windows 7.

WORKAROUND: None

### Internet Explorer bookmarks don't appear in the Internet Explorer smartbar

When Internet Explorer bookmarks roam from one computer to another computer, the index on the second computer can't update, so when typing in the address bar, the favorite won't appear as a possible search result on computer 2.

WORKAROUND: None
