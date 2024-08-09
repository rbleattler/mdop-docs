---
title: How to determine BitLocker encryption state of lost computers
description: Use this procedure with the Administration and Monitoring website to determine the last known BitLocker encryption status of lost or stolen computers and whether the volumes on a lost or stolen computer were encrypted.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to determine BitLocker encryption state of lost computers

Use this procedure with the Administration and Monitoring Website to determine the last known BitLocker encryption status of lost or stolen computers. You can also use it to see whether the volumes on a lost or stolen computer were encrypted.

To complete this task, you need access to the **Reports** area of the Administration and Monitoring Website. To get access to this area, you must be assigned the MBAM Report Users role. You might have given these roles different names when you created them. For more information, see [Planning for MBAM 2.5 groups and accounts](planning-for-mbam-25-groups-and-accounts.md#bkmk-helpdesk-roles).

> [!NOTE]
> Device compliance is determined by the BitLocker policies that your enterprise has deployed. Before you try to determine the BitLocker encryption state of a device, verify your deployed policies.

## To determine the last known BitLocker encryption state of lost computers

1.  Open a web browser and navigate to the **Administration and Monitoring Website**.

2.  In the left pane, select **Reports** to open the Reports page.

3.  Select the **Computer Compliance Report**.

4.  Use the filter fields in the right pane to narrow the search results, and then select **Search**. Results are shown under your search query.

5.  Take the appropriate action, as determined by your policy for lost devices.

## Related articles

[Performing BitLocker Management with MBAM 2.5](performing-bitlocker-management-with-mbam-25.md)
