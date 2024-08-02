---
title: High level architecture for App-V 5.1
description: Use the following information to help you simplify your Microsoft Application Virtualization (App-V) 5.1 deployment.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# High level architecture for App-V 5.1

Use the following information to help you simplify your Microsoft Application Virtualization (App-V) 5.1 deployment.

## Architecture overview

A typical App-V 5.1 implementation consists of the following elements:

| Element | More information |
|--|--|
| App-V 5.1 management server | The App-V 5.1 management server provides overall management functionality for the App-V 5.1 infrastructure. Additionally, you can install more than one instance of the management server in your environment, which provides the following benefits: <ul><li>Fault Tolerance and High Availability - Installing and configuring the App-V 5.1 management server on two separate computers can help in situations when one of the servers is unavailable or offline. <br>You can also help increase App-V 5.1 availability by installing the management server on multiple computers. In this scenario, a network load balancer should also be considered so that server requests are balanced.</li><li>Scalability - You can add other management servers as necessary to support a high load, for example you can install multiple servers behind a load balancer.</li></ul> |
| App-V 5.1 publishing server | The App-V 5.1 publishing server provides functionality for virtual application hosting and streaming. The publishing server doesn't require a database connection and supports the following protocols: <ul><li>HTTP, and HTTPS</li></ul> <br>You can also help increase App-V 5.1 availability by installing the publishing server on multiple computers. A network load balancer should also be considered so that server requests are balanced. |
| App-V 5.1 reporting server | The App-V 5.1 reporting server enables authorized users to run and view existing App-V 5.1 reports and other reports that can help them manage the App-V 5.1 infrastructure. The reporting server requires a connection to the App-V 5.1 reporting database. You can also help increase App-V 5.1 availability by installing the reporting server on multiple computers. A network load balancer should also be considered so that server requests are balanced. |
| App-V 5.1 client | The App-V 5.1 client enables packages created using App-V 5.1 to run on target computers. |

> [!NOTE]
> If you use App-V 5.1 with electronic software distribution (ESD), you aren't required to use the App-V 5.1 management server. You can still use the reporting and streaming functionality of App-V 5.1.

## Related articles

[Getting Started with App-V 5.1](getting-started-with-app-v-51.md)
