---
title: App-V 5.1 Capacity Planning
description: The following recommendations can be used as a baseline to help determine capacity planning information that is appropriate to your organization's App-V 5.1 infrastructure.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# App-V 5.1 Capacity Planning

The following recommendations can be used as a baseline to help determine capacity planning information that is appropriate to your organization's App-V 5.1 infrastructure.

> [!IMPORTANT]
> Use the information in this section only as a general guide for planning your App-V 5.1 deployment. Your system capacity requirements will depend on the specific details of your hardware and application environment. Additionally, the performance numbers displayed in this document are examples and your results may vary.

## Determine the project scope

Before you design the App-V 5.1 infrastructure, you must determine the project's scope. The scope consists of determining which applications will be available virtually and to also identify the target users, and their locations. This information will help determine what type of App-V 5.1 infrastructure should be implemented. Decisions about the scope of the project must be based on the specific needs of your organization.

| Task | More Information |
|--|--|
| Determine Application Scope | Depending on the applications to be virtualized, the App-V 5.1 infrastructure can be set up in different ways. The first task is to define what applications you want to virtualize. |
| Determine Location Scope | Location scope refers to the physical locations (for example, enterprise-wide or a specific geographic location) where you plan to run the virtualized applications. It can also refer to the user population (for example, a single department) who will run the virtual applications. You should obtain a network map that includes the connection paths as well as available bandwidth to each location and the number of users using virtualized applications and the WAN link speed. |

## Determine which App-V 5.1 infrastructure is required

> [!IMPORTANT]
> Both of the following models require the App-V 5.1 client to be installed on the computer where you plan to run virtual applications.

You can also manage your App-V 5.1 environment using an Electronic Software Distribution (ESD) solution such as Microsoft Systems Center Configuration Manager. For more information see [How to deploy App-V 5.1 Packages Using Electronic Software Distribution](how-to-deploy-app-v-51-packages-using-electronic-software-distribution.md).

- **Standalone Model** - The standalone model allows virtual applications to be Windows Installer-enabled for distribution without streaming. App-V 5.1 in Standalone Mode consists of the sequencer and the client; no additional components are required. Applications are prepared for virtualization using a process called sequencing. For more information see, [Planning for the App-V 5.1 Sequencer and Client Deployment](planning-for-the-app-v-51-sequencer-and-client-deployment.md). The stand-alone model is recommended for the following scenarios:

  - With disconnected remote users who cannot connect to the App-V 5.1 infrastructure.

  - When you are running a software management system, such as Configuration Manager 2012.

  - When network bandwidth limitations inhibit electronic software distribution.

- **Full Infrastructure Model** - The full infrastructure model provides for software distribution, management, and reporting capabilities; it also includes the streaming of applications across the network. The App-V 5.1 Full Infrastructure Model consists of one or more App-V 5.1 management servers. The Management Server can be used to publish applications to all clients. The publishing process places the virtual application icons and shortcuts on the target computer. It can also stream applications to local users. For more information about installing the management server see, [Planning for the App-V 5.1 Server Deployment](planning-for-the-app-v-51-server-deployment.md). The full infrastructure model is recommended for the following scenarios:

  > [!IMPORTANT]
  > The App-V 5.1 full infrastructure model requires Microsoft SQL Server to store configuration data. For more information see [App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md).

  - When you want to use the Management Server to publish the application to target computers.

  - For rapid provisioning of applications to target computers.

  - When you want to use App-V 5.1 reporting.

## End-to-end Server Sizing Guidance

The following section provides information about end-to-end App-V 5.1 sizing and planning. For more specific information, refer to the subsequent sections.

> [!NOTE]
> Round trip response time on the client is the time taken by the computer running the App-V 5.1 client to receive a successful notification from the publishing server. Round trip response time on the publishing server is the time taken by the computer running the publishing server to receive a successful package metadata update from the management server.

- 20,000 clients can target a single publishing server to obtain the package refreshes in an acceptable round trip time. (&lt;3 seconds)

- A single management server can support up to 50 publishing servers for package metadata refreshes in an acceptable round trip time. (&lt;5 seconds)

## <a href="" id="---------app-v-5-1-management-server-capacity-planning-recommendations"></a> App-V 5.1 management server capacity planning recommendations

The App-V 5.1 publishing servers require the management server for package refresh requests and package refresh responses. The management server then sends the information to the management database to retrieve information. For more information about App-V 5.1 management server supported configurations see [App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md).

> [!NOTE]
> The default refresh time on the App-V 5.1 publishing server is ten minutes.

When multiple simultaneous publishing servers contact a single management server for package metadata refreshes, the following three factors influence the round trip response time on the publishing server:

1.  Number of publishing servers making simultaneous requests.

2.  Number of connection groups configured on the management server.

3.  Number of access groups configured on the management server.

The following table displays more information about each factor that impacts round trip time.

> [!NOTE]
> Round trip response time is the time taken by the computer running the App-V 5.1 publishing server to receive a successful package metadata update from the management server.

| Factors impacting round trip response time | More Information |
|--|--|
| The number of publishing servers simultaneously requesting package metadata refreshes. | - A single management server can respond to up to 320 publishing servers requesting publishing metadata simultaneously. |
|  | - Round trip response time for 320 pub servers is ~40 seconds. |
|  | - For <50 publishing servers requesting metadata simultaneously, the round trip response time is <5 seconds. |
|  | - From 50 to 320 publishing servers, the response time increases linearly (approximately 2x). |
| The number of connection groups configured on the management server. | - For up to 100 connection groups, there is no significant change in the round trip response time on the publishing server. |
|  | - For 100 - 400 connection groups, there is a minor linear increase in the round trip response time. |
| The number of access groups configured on the management server. | - For up to 40 access groups, there is a linear (approximately 3x) increase in the round trip response time on the publishing server. |

The following table displays sample values for each of the previous factors. In each variation, 120 packages are refreshed from the App-V 5.1 management server.

| Scenario | Variation | Number of connection groups | Number of access groups | Number of publishing servers | Network connection type publishing server / management server | Round trip response time on the publishing server (in seconds) | CPU utilization on management server |
|--|--|--|--|--|--|--|--|
| Publishing servers simultaneously contacting management server for publishing metadata. | Number of publishing servers | 0 | 1 | 50 | LAN | 5 | 17 |
|  |  | 0 | 1 | 100 | LAN | 10 | 17 |
|  |  | 0 | 1 | 200 | LAN | 19 | 17 |
|  |  | 0 | 1 | 300 | LAN | 32 | 15 |
|  |  | 0 | 1 | 315 | LAN | 30 | 17 |
|  |  | 0 | 1 | 320 | LAN | 37 | 15 |
| Publishing metadata contains connection groups | Number of connection groups | 10 | 1 | 100 | LAN | 10 | 17 |
|  |  | 50 | 1 | 100 | LAN | 11 | 19 |
|  |  | 100 | 1 | 100 | LAN | 11 | 22 |
|  |  | 150 | 1 | 100 | LAN | 16 | 19 |
|  |  | 300 | 1 | 100 | LAN | 22 | 20 |
|  |  | 400 | 1 | 100 | LAN | 25 | 20 |
| Publishing metadata contains access groups | Number of access groups | 0 | 1 | 100 | LAN | 10 | 17 |
|  |  | 0 | 10 | 100 | LAN | 43 | 26 |
|  |  | 0 | 20 | 100 | LAN | 153 | 24 |
|  |  | 0 | 40 | 100 | LAN | 535 | 24 |

The CPU utilization of the computer running the management server is around 25% irrespective of the number of publishing servers targeting it. The Microsoft SQL Server database transactions/sec, batch requests/sec and user connections are identical irrespective of the number of publishing servers. For example: Transactions/sec is ~30, batch requests ~200, and user connects ~6.

Using a geographically distributed deployment, where the management server & publishing servers utilize a slow link network between them, the round trip response time on the publishing servers is within acceptable time limits (&lt;5 seconds), even for 100 simultaneous requests on a single management server.

| Scenario | Variation | Number of connection groups | Number of access groups | Number of publishing servers | Network connection type publishing server / management server | Round trip response time on the publishing server (in seconds) | CPU utilization on management server |
|--|--|--|--|--|--|--|--|
| Network connection between the publishing server and management server | 1.5 Mbps Slow link Network | 0 | 1 | 50 | 1.5Mbps Cable DSL | 4 | 1 |
|  |  | 0 | 1 | 100 | 1.5Mbps Cable DSL | 5 | 2 |
| Network connection between the publishing server and management server | LAN / WIFI Network | 0 | 1 | 100 | Wifi | 11 | 15 |
|  |  | 0 | 1 | 200 | Wifi | 20 | 17 |

Whether the management server and publishing servers are connected over a slow link network, or a high speed network, the management server can handle approximately 15,000 package refresh requests in 30 minutes.

## <a href="" id="---------app-v-5-1-reporting-server-capacity-planning-recommendations"></a> App-V 5.1 reporting server capacity planning recommendations

App-V 5.1 clients send reporting data to the reporting server. The reporting server then records the information in the Microsoft SQL Server database and returns a successful notification back to the computer running App-V 5.1 client. For more information about App-V 5.1 Reporting Server supported configurations see [App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md).

> [!NOTE]
> Round trip response time is the time taken by the computer running the App-V 5.1 client to send the reporting information to the reporting server and receive a successful notification from the reporting server.

| Scenario | Summary |
|--|--|
| Multiple App-V 5.1 clients send reporting information to the reporting server simultaneously. | - Round trip response time from the reporting server is 2.6 seconds for 500 clients. |
|  | - Round trip response time from the reporting server is 5.65 seconds for 1000 clients. |
|  | - Round trip response time increases linearly depending on number of clients. |
| Requests per second processed by the reporting server. | - A single reporting server and a single database can process a maximum of 139 requests per second. The average is 121 requests/second. |
|  | - Using two reporting servers reporting to the same Microsoft SQL Server database, the average requests/second is similar to a single reporting server = ~127, with a max of 278 requests/second. |
|  | - A single reporting server can process 500 concurrent/active connections. |
|  | - A single reporting server can process a maximum of 1500 concurrent connections. |
| Reporting Database. | - Lock contention on the computer running Microsoft SQL Server is the limiting factor for requests/second. |
|  | - Throughput and response time are independent of database size. |

### Calculating random delay

The random delay specifies the maximum delay (in minutes) for data to be sent to the reporting server. When the scheduled task is started, the client generates a random delay between **0** and **ReportingRandomDelay** and will wait the specified duration before sending data.

Random delay = 4 \* number of clients / average requests per second.

Example: For 500 clients, with 120 requests per second, the Random delay is, 4 \* 500 / 120 = ~17 minutes.

## <a href="" id="---------app-v-5-1-publishing-server-capacity-planning-recommendations"></a> App-V 5.1 publishing server capacity planning recommendations

Computers running the App-V 5.1 client connect to the App-V 5.1 publishing server to send a publishing refresh request and to receive a response. Round trip response time is measured on the computer running the App-V 5.1 client. Processor time is measured on the publishing server. For more information about App-V 5.1 Publishing Server supported configurations see [App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md).

The following list displays the main factors to consider when setting up the App-V 5.1 publishing server:

- The number of clients connecting simultaneously to a single publishing server.

- The number of packages in each refresh.

- The available network bandwidth in your environment between the client and the App-V 5.1 publishing server.

| Scenario | Summary |
|--|--|
| Multiple App-V 5.1 clients connect to a single publishing server simultaneously. | - A publishing server running dual core processors can respond to at most 5000 clients requesting a refresh simultaneously. |
|  | - For 5000-10000 clients, the publishing server requires a minimum quad core. |
|  | - For 10000-20000 clients, the publishing server should have dual quad cores for more efficient response times. |
|  | - A publishing server with a quad core can refresh up to 10000 packages within 3 seconds. (Supporting 10000 simultaneous clients) |
| Number of packages in each refresh. | - Increasing number of packages will increase response time by ~40% (up to 1000 packages). |
| Network between the App-V 5.1 client and the publishing server. | - Across a slow network (1.5 Mbps bandwidth), there is a 97% increase in response time compared to LAN (up to 1000 users). |

> [!NOTE]
> The publishing server CPU usage is always high during the time interval when it has to process simultaneous requests (&gt;90% in most cases). The publishing server can handle ~1500 client requests in 1 second.

| Scenario | Variation | Number of App-V 5.1 clients | Number of packages | Processor configuration on the publishing server | Network connection type publishing server / App-V 5.1 client | Round trip time on the App-V 5.1 client (in seconds) | CPU utilization on publishing server (in %) |
|--|--|--|--|--|--|--|--|
| App-V 5.1 client sends publishing refresh request & receives response, each request containing 120 packages | Number of clients | 100 | 120 | Dual Core | LAN | 1 | 100 |
|  |  | 1000 | 120 | Dual Core | LAN | 2 | 99 |
|  |  | 5000 | 120 | Quad Core | LAN | 2 | 89 |
|  |  | 10000 | 120 | Quad Core | LAN | 3 | 77 |
| Multiple packages in each refresh | Number of packages | 1000 | 500 | Quad Core | LAN | 2 | 92 |
|  |  | 1000 | 1000 | Quad Core | LAN | 3 | 91 |
| Network between client and publishing server | 1.5 Mbps Slow link network | 100 | 120 | Quad Core | 1.5 Mbps Intra-Continental Network | 3 |  |
|  |  | 500 | 120 | Quad Core | 1.5 Mbps Intra-Continental Network | 10 (with 0.2% failure rate) |  |
|  |  | 1000 | 120 | Quad Core | 1.5 Mbps Intra-Continental Network | 17 (with 1% failure rate) |  |

## <a href="" id="---------app-v-5-1-streaming-capacity-planning-recommendations"></a> App-V 5.1 streaming capacity planning recommendations

Computers running the App-V 5.1 client stream the virtual application package from the streaming server. Round trip response time is measured on the computer running the App-V 5.1 client, and is the time taken to stream the entire package.

The following list identifies the main factors to consider when setting up the App-V 5.1 streaming server:

- The number of clients streaming application packages simultaneously from a single streaming server.

- The size of the package being streamed.

- The available network bandwidth in your environment between the client and the streaming server.

| Scenario | Summary |
|--|--|
| Multiple App-V 5.1 clients stream applications from a single streaming server simultaneously. | - If the number of clients simultaneously streaming from the same server increases, there is a linear relationship with the package download/streaming time. |
| Size of the package being streamed. | - The package size has a significant impact on the streaming/download time only for larger packages with a size ~ 1GB. For package sizes ranging from 3 MB to 100 MB, the streaming time ranges from 20 seconds to 100 seconds, with 100 simultaneous clients. |
| Network between the App-V 5.1 client and the streaming server. | - Across a slow network (1.5 Mbps bandwidth), there is a 70-80% increase in response time compared to LAN (up to 100 users). |

The following table displays sample values for each of the factors in the previous list:

| Scenario | Variation | Number of App-V 5.1 clients | Size of each package | Network connection type streaming server / App-V 5.1 client | Round trip time on the App-V 5.1 client (in seconds) |
|--|--|--|--|--|--|
| Multiple App-V 5.1 clients streaming virtual application packages from a streaming server. | Number of clients. | 100 | 3.5 MB | LAN | 29 |
|  |  | 200 | 3.5 MB | LAN | 39 |
|  |  | 1000 | 3.5 MB | LAN | 391 |
|  |  | 100 | 5 MB | LAN | 35 |
|  |  | 200 | 5 MB | LAN | 68 |
|  |  | 1000 | 5 MB | LAN | 461 |
| Size of each package being streamed. | Size of each package. | 100 | 21 MB | LAN | 33 |
|  |  | 200 | 21 MB | LAN | 83 |
|  |  | 100 | 109 MB | LAN | 100 |
|  |  | 200 | 109 MB | LAN | 160 |
| Network connection between client and App-V 5.1 streaming server. | 1.5 Mbps Slow link network. | 100 | 3.5 MB | 1.5 Mbps Intra-Continental Network | 102 |
|  |  | 100 | 5 MB | 1.5 Mbps Intra-Continental Network | 121 |

Each App-V 5.1 streaming server should be able to handle a minimum of 200 clients concurrently streaming virtualized applications.

> [!NOTE]
> The actual time to it will take to stream is determined primarily by the number of clients streaming simultaneously, number of packages, package size, the server's network activity, and network conditions.

For example, an average user can stream a 100 MB package in less than 2 minutes, when 100 simultaneous clients are streaming from the server. However, a package of size 1 GB could take up to 30 minutes. In most real world environments streaming demand is not uniformly distributed, you will need to understand the approximate peak streaming requirements present in your environment in order to properly size the number of required streaming servers.

The number of clients a streaming server can support can be significantly increased and the peak streaming requirements reduced if you pre-cache your applications. You can also increase the number of clients a streaming server can support by using on-demand streaming delivery and stream optimized packages.

## Combining App-V 5.1 Server Roles

Discounting scaling and fault-tolerance requirements, the minimum number of servers needed for a location with connectivity to Active Directory is one. This server will host the management server, management server service, and Microsoft SQL Server roles. Server roles, therefore, can be arranged in any desired combination since they do not conflict with one another.

Ignoring scaling requirements, the minimum number of servers necessary to provide a fault-tolerant implementation is four. The management server, and Microsoft SQL Server roles support being placed in fault-tolerant configurations. The management server service can be combined with any of the roles, but remains a single point of failure.

Although there are a number of fault-tolerance strategies and technologies available, not all are applicable to a given service. Additionally, if App-V 5.1 roles are combined, certain fault-tolerance options may no longer apply due to incompatibilities.

## Related topics

[App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md)

[Planning for High Availability with App-V 5.1](planning-for-high-availability-with-app-v-51.md)
