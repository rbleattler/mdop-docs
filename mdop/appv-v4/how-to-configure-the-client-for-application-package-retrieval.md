---
title: How to configure the client for application package retrieval
description: How to configure the client for application package retrieval.
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.date: 06/16/2016
---

# How to configure the client for application package retrieval

When the client is configured with an Application Virtualization (App-V) Management Server as its publishing server, by default at the next publishing refresh cycle, the client retrieves from the server the Open Software Descriptor (OSD) and package manifest files for each package that the user is authorized to use. The client uses the package source information that is defined in these files to determine where to find the package content, icons, and file type associations.

If you want the client to obtain the package content (SFT file) from a local App-V Streaming Server or other alternate source such as a Web server or file server, instead of from the App-V Management Server, you can configure the ApplicationSourceRoot registry key value on the computer to point to the local content share on the other server. The OSD file still defines the original source path for the package content. However the client uses the value of the ApplicationSourceRoot setting in place of the server and share that are specified in the content path in the OSD file. This redirects the client to retrieve the content from the other server.

You can also configure the OSDSourceRoot and IconSourceRoot registry key values if you want to override those settings in the package manifest file or in the paths sent by a publishing server. The OSDSourceRoot specifies a source location for OSD file retrieval for an application package during publication. The IconSourceRoot specifies a source location for icon retrieval for an application package during publication.

> [!NOTE]
>
> - The IconSourceRoot and OSDSourceRoot settings override the values in the package manifest file, so if you try to deploy a package by using the Windows Installer (.msi) file method, it will also override the values in the package manifest file that is contained within that .msi file.
>
> - During both the publishing and HTTP(S) streaming operations,App-V 4.5 SP1 clients use the proxy server settings that are configured in Internet Explorer on the user's computer.

## Configure the ApplicationSourceRoot registry key value

- Configure the ApplicationSourceRoot in the following registry key value with either a UNC path or a URL:

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SoftGrid\4.5\Client\Configuration\ApplicationSourceRoot`

    The correct format for the Universal Naming Convention (UNC) path is `\\computername\sharefolder\<folder>\`, where **folder** is optional. The **computername** can be a Fully Qualified Domain Name (FQDN) or an IP address, and **sharefolder** can be a drive letter. Only the `\\computername\sharedfolder` or drive letter portion of the OSD path is replaced.

    The correct format for the URL path is **protocol://servername:\[port\]\[/path\]\[/\]**, where **port** and **path** are optional. If **port** isn't specified, the default port for the protocol is used. Only the **protocol://server:port** portion of the OSD URL is replaced.

    > [!IMPORTANT]
    > Environment variables aren't supported in the ApplicationSourceRoot definition.

The following table lists examples of acceptable URL and UNC path formats.

| ApplicationSourceRoot | OSD File HREF Path | Result | Comments |
|--|--|--|--|
| `rtsps://mainserver:322` | `rtsp://appserver/productivity/office2k3.sft?customer=seq` | `rtsps://mainserver:322/productivity/office2k3.sft?customer=seq` |  |
| `rtsps://mainserver:322/prodapps` | `rtsp://appserver/productivity/office2k3.sft?customer=seq` | `rtsps://mainserver:322/prodapps/productivity/office2k3.sft?customer=seq` |  |
| `https://mainserver:443/prodapps` | `rtsp://appserver/productivity/office2k3.sft?customer=seq` | `https://mainserver:443/prodapps/productivity/office2k3.sft?customer=seq` |  |
| `rtsps://mainserver:322/prodapps` | `rtsp://%SFT_APPVSERVER%:554/productivity/office2k3.sft?customer=seq` | `rtsps://mainserver:322/prodapps/productivity/office2k3.sft?customer=seq` |  |
| `rtsps://mainserver:322` | `\\uncserver\share\productivity\office2k3.sft` | `rtsps://mainserver:322/productivity/office2k3.sft` | `\` converted to `/` |
| `rtsps://mainserver:322` | `file://\\uncserver\share\productivity\office2k3.sft` | `rtsps://mainserver:322/productivity/office2k3.sft` | `\` converted to `/` |
| `\\uncserver\share` | `rtsp://appserver/productivity/office2k3.sft?customer=seq` | `\\uncserver\share\productivity\office2k3.sft` | `/` converted to `\` and parameter dropped when converting to UNC path |
| `\\uncserver\share\prodapps` | `rtsp://appserver/productivity/office2k3.sft?customer=seq` | `\\uncserver\share\prodapps\productivity/office2k3.sft` | `/` converted to `\` and parameter dropped when converting to UNC path |
| `M:` | `\\uncserver\share\productivity\office2k3.sft` | `M:\productivity\office2k3.sft` |  |
| `M:\prodapps` | `\\uncserver\share\productivity\office2k3.sft` | `M:\prodapps\productivity/office2k3.sft` |  |

## configure the OSDSourceRoot value

-   Configure the OSDSourceRoot in the following registry key value with either a UNC path or a URL:

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SoftGrid\4.5\Client\Configuration\OSDSourceRoot`

    Acceptable formats for the OSDSourceRoot include UNC paths and URLs, as in the following example:

    - `\\computername\sharefolder\resource` or `\\computername\content` or `C:\foldername`

    - `https://computername/productivity/`

**To configure the IconSourceRoot value**

-   Configure the IconSourceRoot in the following registry key value with either a UNC path or a URL:

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SoftGrid\4.5\Client\Configuration\IconSourceRoot`

    Acceptable formats for the IconSourceRoot include UNC paths and URLs, as in the following example:

    - `\\computername\sharefolder\resource` or `\\computername\content` or `C:\foldername`

    - `https://computername/productivity/`

## Related information

[How to configure the App-V client registry settings by using the command line](how-to-configure-the-app-v-client-registry-settings-by-using-the-command-line.md)

