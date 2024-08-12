---
title: Monitoring web service request performance counters
description: Microsoft BitLocker Administration and Monitoring (MBAM) provides performance counters that record the performance of requests that are sent to web services.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Monitoring web service request performance counters

Microsoft BitLocker Administration and Monitoring (MBAM) provides performance counters that record the performance of requests that are sent to the following web services:

- **StatusReportingService.svc** - service that receives requests for compliance status

- **CoreService.svc** - service that receives requests for key recovery attempts

## Performance counters that MBAM provides

MBAM provides the following performance counters for each of the public methods that it implements by its StatusReportingService and CoreService web services:

| Type of performance counter | Description |
|--|--|
| Total number of requests | Provides an incrementing count that starts from zero when the server is started or restarted. <br> Provides an overall view of system activity. You can monitor it by automated tools to ensure the health of the server and to validate that the counter continually increments over a specified period of time. |
| Requests per second | Indicates the current throughput of the MBAM server as it supports the MBAM client base. <br> Enables site administrators to: <ul><li>Calculate the average number of requests per second, based on the number of MBAM clients and their reporting frequency.</li><li>Validate that the number of requests per second broadly correlates with the calculated average number of requests per second. A significant variance can indicate that the MBAM client isn't installed on a percentage of the client base or that an MBAM group policy object isn't successfully deployed.</li></ul> |
| Request duration | Records the duration of requests in milliseconds. <br> Although this counter is updated with the duration of each request, Windows Performance Monitor samples it only periodically (typically every second), so you might see some variability in the value. For this reason, consider using the average value displayed by Performance Monitor. |

## Performance counter results and recommendations

As you add new MBAM clients to an MBAM server with spare capacity, expect to see an increase in the number of requests per second. This increase is proportional to the number of new client computers. The average request duration remains relatively static. As the server nears its maximum capacity, the requests per second start to level out, and the average request duration starts to get longer.

If you're concerned about whether your MBAM servers can support your client base, consider deploying MBAM in phases across different collections of client computers. As you deploy MBAM to each collection of client computers, we recommend that you take snapshots of the performance counters to see the relative effect of deploying to each new client collection. If the number of requests per second starts to level off and the average request duration increases, consider enhancing your MBAM server infrastructure by doing one of the following actions:

- Moving the MBAM database onto a dedicated Microsoft SQL Server or SQL Server cluster

- Load-balancing MBAM across multiple Internet Information Services (IIS) web servers

- Deploying MBAM on more powerful server hardware

## Viewing performance counters

The recommended tool for viewing MBAM performance counters is Windows Performance Monitor, which comes with Windows. If you use Windows PowerShell, you don't need to enable the counters before viewing them. The Windows PowerShell cmdlet **Enable-WebApplication** automatically registers the counters.

For detailed instructions on how to view performance counters, see [How to view MBAM performance counters](/archive/technet-wiki/24247.how-to-view-performance-counters-for-mbam-2-5).

## Related articles

[Maintaining MBAM 2.5](maintaining-mbam-25.md)
