---
title: Ensure that crash analyzer can access symbol files
description: How to ensure that crash analyzer can access symbol files.
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---


# Ensure that crash analyzer can access symbol files

Typically, debugging information is stored in a symbol file that is separate from the program. You must have access to the symbol information when you debug an application that has stopped responding.

Symbol files are automatically downloaded when you run **Crash Analyzer**. If the computer doesn't have an Internet connection or the network requires the computer to access an HTTP proxy server, the symbol files can't be downloaded.

To ensure that Crash Analyzer can access symbol files, you can do one of the following:

- **Copy the dump file to another computer.** If the symbols can't be downloaded because of a lack of an Internet connection, copy the memory dump file to a computer that does have an Internet connection and run the stand-alone **Crash Analyzer Wizard** on that computer.

- **Access the symbol files from another computer.** If the symbols can't be downloaded because of a lack of an Internet connection, you can download the symbols from a computer that does have an Internet connection and then copy them to the computer that doesn't have an Internet connection, or you can map a network drive to a location where the symbols are available on the local network. If you run the **Crash Analyzer** in a Windows Recovery Environment (Windows RE), you can include the symbol files on the Microsoft Diagnostics and Recovery Toolset (DaRT) 10 recovery image.

- **Access symbol files through an HTTP proxy server.** If the symbols can't be downloaded because an HTTP proxy server must be accessed, use the following steps to access an HTTP proxy server. In DaRT 10, the **Crash Analyzer Wizard** has a setting available on the **Specify Symbol Files Location** dialog page, marked with the label **Proxy server (optional, using the format "server:port")**. You can use this text box to specify a proxy server. Enter the proxy address in the form **&lt;hostname&gt;:&lt;port&gt;**, where the &lt;**hostname**&gt; is a DNS name or IP address, and the &lt;**port**&gt; is a TCP port number. There are two modes in which the **Crash Analyzer** can be run. Following is how you use the proxy setting in each of these modes:

    - **Online mode:** In this mode, if the proxy server field is left blank, the wizard uses the proxy settings from Internet Options in Control Panel. If you enter a proxy address in the text box, it uses that address, and it overrides the setting in the Internet Options.

    - Windows Recovery Environment (Windows RE): When you run **Crash Analyzer** from the **Diagnostics and Recovery Toolset** window, there's no default proxy address. If the computer is directly connected to the Internet, a proxy address isn't required. Therefore, you can leave this field blank in the wizard setting. If the computer isn't directly connected to the Internet, and it is in a network environment that has a proxy server, you must set the proxy field in the wizard to access the symbol store. The proxy address can be obtained from the network administrator. Setting the proxy server is important only when the public symbol store is connected to the Internet. If the symbols are already on the DaRT recovery image, or if they're available locally, setting the proxy server isn't required.

## Related information

- [Diagnosing System Failures with Crash Analyzer](diagnosing-system-failures-with-crash-analyzer-dart-10.md)
- [Operations for DaRT 10](operations-for-dart-10.md)
