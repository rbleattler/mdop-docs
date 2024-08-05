---
title: View App-V server publishing metadata
description: Use this procedure to view publishing metadata, which can help you resolve publishing-related issues.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# View App-V server publishing metadata

Use this procedure to view publishing metadata, which can help you resolve publishing-related issues. You must be using the App-V Management server to use this procedure.

## <a href="" id="bkmk-51-reqs-pub-meta"></a>App-V 5.1 requirements for viewing publishing metadata

In App-V 5.1, you must provide the following values in the address when you query the App-V Publishing server for metadata:

| Value | Additional details |
|--|--|
| **ClientVersion** | If you omit the **ClientVersion** parameter from the query, the metadata excludes the features that were new in App-V 5.0 SP3. |
| **ClientOS** | You have to provide this value only if you select specific client operating systems when you sequence the package. If you select the default (all operating systems), do not specify this value in the query.<br><br>If you omit the **ClientOS** parameter from the query, only the packages that were sequenced to support any operating system appear in the metadata. |

## <a href="" id="bkmk-syntax-view-pub-meta"></a>Query syntax for viewing publishing metadata

Query syntax: `http://<PubServer>:<Publishing Port#>/?ClientVersion=<AppvClientVersion>&ClientOS=<OSStringValue>`

| Parameter                        | Description                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| `<PubServer>`                    | Name of the App-V Publishing server.                                        |
| `<Publishing Port#>`             | Port to the App-V Publishing server, which you defined when you configured the Publishing server. |
| `ClientVersion=<AppvClientVersion>` | Version of the App-V client. Refer to the following table for the correct value to use. |
| `ClientOS=<OSStringValue>`       | Operating system of the computer that is running the App-V client. Refer to the following table for the correct value to use. |

To get the name of the Publishing server and the port number (`http://<PubServer>:<Publishing Port#>`) from the App-V Client, look at the URL configuration of the **Get-AppvPublishingServer** PowerShell cmdlet.

### Example

`http://pubsvr01:2718/?clientversion=5.0.10066.0&clientos=WindowsClient_6.2_x64`

In the example:

- A Windows Server 2012 R2 named "pubsvr01" hosts the Publishing service.
- The Windows client is Windows 8.1 64-bit.

## <a href="" id="bkmk-values-query-pub-meta"></a>Query values for client operating system and version

In your publishing metadata query, enter the string values that correspond to the client operating system and version that you're using.

| Operating system        | Architecture | Operating string value     |
|-------------------------|--------------|----------------------------|
| Windows 10              | 64-bit       | WindowsClient_10.0_x64     |
| Windows 10              | 32-bit       | WindowsClient_10.0_x86     |
| Windows 8.1             | 64-bit       | WindowsClient_6.2_x64      |
| Windows 8.1             | 32-bit       | WindowsClient_6.2_x86      |
| Windows 8               | 64-bit       | WindowsClient_6.2_x64      |
| Windows 8               | 32-bit       | WindowsClient_6.2_x86      |
| Windows Server 2012 R2  | 64-bit       | WindowsServer_6.2_x64      |
| Windows Server 2012 R2  | 32-bit       | WindowsServer_6.2_x86      |
| Windows Server 2012     | 64-bit       | WindowsServer_6.2_x64      |
| Windows Server 2012     | 32-bit       | WindowsServer_6.2_x86      |
| Windows 7               | 64-bit       | WindowsClient_6.1_x64      |
| Windows 7               | 32-bit       | WindowsClient_6.1_x86      |
| Windows Server 2008 R2  | 64-bit       | WindowsServer_6.1_x64      |
| Windows Server 2008 R2  | 32-bit       | WindowsServer_6.1_x86      |

## <a href="" id="bkmk-whatis-pub-metadata"></a>Definition of publishing metadata

When packages are published to a computer that is running the App-V client, metadata is sent to that computer indicating which packages and connection groups are being published. The App-V Client makes two separate requests for the following:

- Packages and connection groups that are entitled to the client computer.

- Packages and connection groups that are entitled to the current user.

The Publishing server communicates with the Management server to determine which packages and connection groups are available to the requester. The Publishing server must be registered with the Management server in order for the metadata to be generated.

You can view the metadata for each request in an Internet browser by using a query that is in the context of the specific user or computer.
