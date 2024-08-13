---
title: Editing the MBAM 2.5 group policy settings
description: How to edit the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 group policy settings.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Editing the MBAM 2.5 group policy settings

To successfully deploy Microsoft BitLocker Administration and Monitoring (MBAM), you have to:

- Copy the MBAM 2.5 group policy templates. For more information, see [Copying the MBAM 2.5 group policy templates](copying-the-mbam-25-group-policy-templates.md).
- Determine which group policy objects (GPOs) you want to use in your MBAM implementation. Based on the needs of your organization, you might have to configure other group policy settings. For more information, see [Planning for MBAM 2.5 group policy requirements](planning-for-mbam-25-group-policy-requirements.md). This article contains descriptions of the GPOs.
- Set the group policy settings for your organization.

> [!IMPORTANT]
> Do not change the group policy settings in the **BitLocker Drive Encryption** node, or MBAM will not work correctly. When you configure the group policy settings in the **MDOP MBAM (BitLocker Management)** node, MBAM automatically configures the **BitLocker Drive Encryption** settings for you.

## To edit MBAM client group policy settings

1.  On a computer that has the MBAM group policy templates installed, make sure that MBAM services are enabled.

2.  Using the Group Policy Management Console (GPMC.msc) or the Microsoft Advanced Group Policy Management MDOP product on a computer with the MBAM group policy templates installed, select **Computer configuration** &gt; **Policies** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **MDOP MBAM (BitLocker Management)**.

3.  Edit the group policy settings that are required to enable MBAM client services on client computers. For each policy in the following table, select **Policy Group**, select the **Policy** you want, and then configure the settings.

    | Policy Group            | Policy                                      |
    |-------------------------|---------------------------------------------|
    | Client Management       | Configure MBAM services                     |
    | Operating System Drive  | Operating system drive encryption settings  |
    | Removable Drive         | Control use of BitLocker on removable drives|
    | Fixed Drive             | Control use of BitLocker on fixed drives    |

## Related articles

[Planning for MBAM 2.5 group policy requirements](planning-for-mbam-25-group-policy-requirements.md)

[Copying the MBAM 2.5 group policy templates](copying-the-mbam-25-group-policy-templates.md)
