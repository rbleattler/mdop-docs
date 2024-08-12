---
title: How to configure the Self-Service Portal when client computers can't access the Microsoft content delivery network
description: Follow these instructions if the client computers in your organization don't have access to the Microsoft Ajax content delivery network (CDN).
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# How to configure the Self-Service Portal when client computers can't access the Microsoft content delivery network

Follow these instructions if the client computers in your organization don't have access to the Microsoft Ajax content delivery network (CDN).

## Why you need to configure this

Your client computers need access to the CDN, which gives the Self-Service Portal the required access to certain JavaScript files. If you don't configure the Self-Service Portal when client computers can't access CDN, it only displays the company name and the account under which the user signs in. It doesn't show any error message.

> [!NOTE]
> In MBAM 2.5 SP1, the JavaScript files are included in the product, and you don't need to follow the instructions in this section to configure the SSP to support clients that can't access the internet.

## How to configure the Self-Service Portal when client computers can't access the CDN

1. Download the following JavaScript files from the CDN:

   - [jQuery-1.10.2.min.js](https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js)  <!--aka https://go.microsoft.com/fwlink/?LinkID=390515 -->

   - [jQuery.validate.min.js](https://ajax.aspnetcdn.com/ajax/jquery.validate/1.11.1/jquery.validate.min.js) <!-- https://go.microsoft.com/fwlink/?LinkID=390516 -->

   - [jQuery.validate.unobtrusive.min.js](https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js) <!-- https://go.microsoft.com/fwlink/?LinkID=390517 -->

2. Copy the JavaScript files to the **Scripts** directory of the Self-Service Portal. This directory is located in `<MBAM Self-Service install directory>\Self Service Website\Scripts`.

3. Open Internet Information Services (IIS) Manager.

4. Expand **Sites** > **Microsoft BitLocker Administration and Monitoring**, and highlight **SelfService**.

    > [!NOTE]
    > *SelfService* is the default virtual directory name. If you chose a different name for this directory during the configuration, remember to replace *SelfService* in these instructions with the name you chose.

5. In the middle pane, double-click **Application Settings**.

6. For each item in the following list, edit the application settings to reference the new location by replacing `/<virtual directory>/` with `/SelfService/`, or whatever name you chose during configuration. For example, the virtual directory path is similar to `/selfservice/Scripts/jQuery-1.10.2.min.js`.

    - `jQueryPath`: `/<virtual directory>/Scripts/jQuery-1.10.2.min.js`

    - `jQueryValidatePath`: `/<virtual directory>/Scripts/jQuery.validate.min.js`

    - `jQueryValidateUnobtrusivePath`: `/<virtual directory>/Scripts/jQuery.validate.unobtrusive.min.js`

## Related articles

[How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md)
