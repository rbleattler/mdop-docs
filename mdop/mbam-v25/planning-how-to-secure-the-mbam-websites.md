---
title: Planning how to secure the MBAM websites
description: This article describes methods for securing the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 Administration and Monitoring Website and Self-Service Portal.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Planning how to secure the MBAM websites

This article describes the following methods for securing the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 Administration and Monitoring Website and Self-Service Portal:

| Method | Required or optional? |
|--------|-----------------------|
| Using certificates to secure MBAM websites | Optional, but highly recommended |
| Registering service principal names (SPN) for the application pool account | Required |

For more information about how to secure your MBAM deployment, see [MBAM 2.5 security considerations](mbam-25-security-considerations.md).

## Using certificates to secure MBAM websites

Use a certificate to secure the communication between the:

- MBAM client and the web services

- Browser and the Administration and Monitoring Website and the Self-Service Portal websites

For more information about requesting and installing a certificate, see [Configuring internet server certificates](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731977(v=ws.10)).

> [!NOTE]
> You can configure the websites and web services on different servers only if you use Windows PowerShell. If you use the MBAM Server Configuration wizard to configure the websites, you must configure the websites and the web services on the same server.

To secure the communication between the web services and the databases, we also recommend that you force encryption in SQL Server. For information about securing all connections to SQL Server, including communication between the web services and SQL Server, see [MBAM 2.5 security considerations](mbam-25-security-considerations.md#bkmk-secure-databases).

## Registering SPNs for the application pool account

To enable the MBAM Servers to authenticate communication from the Administration and Monitoring Website and the Self-Service Portal, you must register a Service Principal Name (SPN) for the host name under the domain account that you use for the web application pool.

This section contains instructions on how to register SPNs for the following types of host names:

- Fully qualified domain name

- NetBIOS name

- Virtual name

### Before you create SPNs for an initial MBAM installation

Review the information in the following table before you start creating SPNs.

- **Create a service account in Active Directory Domain Services (ADDS).** The service account is a user account that you create in ADDS to provide security for the MBAM websites. The MBAM websites run under an application pool, whose identity is the name of the service account. The SPNs are then registered in the application pool account.

  > [!NOTE]
  > You must use the same application pool account for all web servers.

- **Verify that either the IIS-IUSRS group account or the application pool account has been granted the necessary rights.** To check this access, follow these steps:
    1. Open the **Local Security Policy editor** and expand the **Local Policies** node.
    2. Select the **User Rights Assignment** node, and double-click the **Impersonate a client after authentication** and **Log on as a batch job** Group Policy settings in the right pane.

- **If you configure the MBAM websites by using a domain administrative account, MBAM will create the SPNs for you.** If you configure the MBAM websites by using a domain administrative account, follow the steps in this article to register SPNs manually for the type of host name that you use.

### Registering SPNs when you use a fully qualified domain host name

If you use a fully qualified domain host name when you configure MBAM, you have to register only one SPN, as shown in the following example.

- Register an SPN for the fully qualified domain name.
  - `Setspn -s http/mybitlockerrecovery.contoso.com contoso\mbamapppooluser`
  - The fully qualified host name is `mybitlockerrecovery.contoso.com`, and the domain account used for the web application pool is `contoso\mbamapppooluser`.
- Configure constrained delegation for the SPN that you register for the application pool account.
  - [Configuring constrained delegation](/previous-versions/tn-archive/cc720385(v=ws.10))
  - This requirement only applies to MBAM 2.5. It isn't necessary in MBAM 2.5 SP1.

### Registering SPNs when you use a NetBIOS host name

If you use a NetBIOS host name when you configure MBAM, register one SPN for the NetBIOS name, and another SPN for the fully qualified domain name, as shown in the following examples.

- Register an SPN for the NetBIOS host name.
  - `Setspn -s http/nbname01 contoso\mbamapppooluser`
  - The NetBIOS host name is `nbname01`, and the domain account used for the web application pool is `contoso\mbamapppooluser`.
- Register an SPN for the fully qualified domain name.
  - `Setspn -s http/nbname01.corp.contoso.com contoso\mbamapppooluser`
  - The fully qualified domain name is `nbname01.contoso.com`, and the domain account used for the web application pool is `contoso\mbamapppooluser`.
- Configure constrained delegation for the SPNs that you register for the application pool account.
  - [Configuring constrained delegation](/previous-versions/tn-archive/cc720385(v=ws.10))
  - This requirement only applies to MBAM 2.5. It isn't necessary in MBAM 2.5 SP1.

### <a href="" id="bkmk-regvirtualspn"></a>Registering SPNs when you use a virtual host name

If you configure MBAM with a virtual host name that is a fully qualified domain name, register only one SPN for the virtual host name. If the virtual host name that you configure isn't a fully qualified domain name, you must create a second SPN that specifies the fully qualified domain name, as described in the following examples.

- If your virtual host name is a fully qualified domain name, as in this example, register only one SPN.
  - `Setspn -s http/mbamvirtual.contoso.com contoso\mbamapppooluser`
  - In the example, the virtual host name is `mbamvirtual.contoso.com`, and the domain account used for the web application pool is `contoso\mbamapppooluser`.
- Register this other SPN if your virtual host name isn't a fully qualified domain name.
  - `Setspn -s http/mbamvirtual contoso\mbamapppooluser`
  - In the example, the virtual host name is `mbamvirtual`, and the domain account used for the web application pool is `contoso\mbamapppooluser`.
- Register this other SPN if your virtual host name isn't a fully qualified domain name.
  - `Setspn -s http/mbamvirtual.contoso.com contoso\mbamapppooluser`
  - In the example, the virtual host name is `mbamvirtual.contoso.com`, and the domain account used for the web application pool is `contoso\mbamapppooluser`.
- On the Domain Name Server (DNS) server, create an "A record" for the custom host name and point it to a web server or a load balancer.
  - Use A records instead of CNAMES. If you use CNAMES to point to the domain address, you must also register SPNs for the web server name in the application pool account.
- Configure constrained delegation for the SPNs that you register for the application pool account.
  - [Configuring constrained delegation](/previous-versions/tn-archive/cc720385(v=ws.10))
  - This requirement only applies to MBAM 2.5. It isn't necessary in MBAM 2.5 SP1.

### <a href="" id="bkmk-registerspn"></a>Registering an SPN when you upgrade from previous versions of MBAM

Complete the steps in this section only if you want to:

- Upgrade from a previous version of MBAM.

- Run the websites in MBAM 2.5 in a load-balanced or distributed configuration, and you currently run in a configuration that isn't load balanced.

If you already registered SPNs on the machine account rather than in an application pool account, MBAM uses the existing SPNs, and you can't configure the websites in a load-balanced or distributed configuration.

- Create an application pool account in Active Directory Domain Services.
- Remove the currently installed websites and web services. For more information, see [Removing MBAM server features or software](removing-mbam-server-features-or-software.md).
- Remove SPNs from the machine account. For example: `Setspn -d http/mbamwebserver mbamwebserver` or `Setspn -d http/mbamwebserver.contoso.com mbamwebserver`
- Register SPNs in the application pool account. Follow the steps for [Registering SPNs when you use a virtual host name](#bkmk-regvirtualspn).
- Reconfigure the web applications and web services. For more information, see [How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md).
- Do one of the following steps, depending on the method you use for the configuration:
  - **MBAM Server Configuration wizard**: Enter the application pool account in the **Web service application pool domain account** field.
  - **Windows PowerShell cmdlet** `Enable-MbamWebApplication`: Enter the account in the `WebServiceApplicationPoolCredential` parameter.

  > [!IMPORTANT]
  > The host name that you enter must be the same name as the virtual host name for which you are creating the SPNs. Also, in your web farm, the host names and the application pool credentials must be the same on every server that you configure.

  When MBAM configures the web applications, it tries to register the SPNs for you. It can only do it if you have Domain Admin rights on the server on which you install MBAM. If you don't have these rights, you can complete the configuration, but you have to set the SPNs before or after you configure MBAM.

## Required request filtering settings

**Allow unlisted file name extensions** is required for the application to operate as expected. To find this setting, go to **Microsoft BitLocker Administration and Monitoring** -> **Request Filtering** -> **Edit Feature Settings**.

## Related articles

[Preparing your environment for MBAM 2.5](preparing-your-environment-for-mbam-25.md)

[MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md)
