---
title: Technical overview of AGPM
description: Microsoft Advanced Group Policy Management (AGPM) is a client/server application. The AGPM server stores group policy objects (GPOs) offline in the archive that AGPM creates on the server's file system.
author: aczechowski
ms.assetid: 36bc0ab5-f752-474c-8559-721ea95169c2
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.pagetype: mdop
ms.mktglfcycl: manage
ms.sitesec: library
ms.date: 08/30/2016
---


# Technical Overview of AGPM

Microsoft Advanced Group Policy Management (AGPM) is a client/server application. The AGPM server stores group policy objects (GPOs) offline in the archive that AGPM creates on the server's file system. Group policy administrators use the AGPM snap-in for the Group Policy Management Console (GPMC) to work with GPOs on the server that hosts the archive.

If you understand the following information, you can improve group policy administrators' effectiveness with AGPM:

- The parts of AGPM and related items.
- How they store GPOs in the file system.
- How permissions control the actions available to each user role.

## Terminology

The following list explains the basic AGPM terms.

- **AGPM client:** A computer that runs the AGPM snap-in for the GPMC and from which group policy administrators manage GPOs.

- **AGPM snap-in:** The software component of AGPM installed on AGPM clients so that they can manage GPOs.

- **AGPM server:** A server that runs the AGPM service and manages an archive. Each AGPM server can manage only one archive, but one AGPM server can manage archive data for multiple domains in one archive. An archive can be hosted on a computer other than an AGPM server.

- **AGPM service:** The software component of AGPM that runs on an AGPM server as a service. The service manages GPOs in the archive and in the production environment in that forest.

- **Archive:** In AGPM, a central store that contains the controlled GPOs that the associated AGPM server manages, in addition to the history for each of those GPOs. This history includes all previous controlled versions of each GPO. An archive consists of an archive index file and associated archive data that might include data for GPOs in multiple domains. An archive can be hosted on a computer other than an AGPM server.

- **Controlled GPO:** A GPO that AGPM manages. AGPM manages the history and permissions of controlled GPOs, which it stores in the archive.

- **Uncontrolled GPO:** A GPO in the production environment for a domain and not managed by AGPM.

## What AGPM installs, creates, and affects

On an AGPM server, the AGPM setup program installs the AGPM service. AGPM doesn't alter the Active Directory directory service or the schema. By default, the AGPM server program files are installed in `%ProgramFiles%\Microsoft\AGPM\Server`. You can install the AGPM service on a domain controller if you have to; however, we recommend that you install the AGPM service on a member server.

On an AGPM client, the AGPM setup program installs the AGPM snap-in, adding a **Change Control** folder to each domain that appears in the GPMC. By default, the AGPM client program files are installed in `%ProgramFiles%\Microsoft\AGPM\Client`.

The following table describes both the items that AGPM installs or creates and the parts of the operating system that affect AGPM operation.

| Item | Description |
|--|--|
| **AGPM service** | The AGPM service runs on the AGPM server. The service manages the archive, which contains offline GPOs, and controlled GPOs in the production environment. The default configuration of the AGPM service is as follows: <ul><li>**Service name:** AGPM service</li><li>**Display name:** AGPM service</li><li>**Path to executable:** `%ProgramFiles%\Microsoft\AGPM\Server\Agpm.exe`</li><li>**Startup:** Automatic</li><li>**Log on as:** AGPM service Account specified during installation of AGPM server, which can be changed using **Programs and Features** in the **Control Panel**.</li></ul> |
| **AGPM archive** | By default, AGPM creates the archive in `%ProgramData%\Microsoft\AGPM` on the AGPM server. The archive provides storage for offline GPOs, and it can store multiple versions of each GPO. Changes that AGPM makes to GPOs in the archive don't affect the production environment until an AGPM administrator or approver deploys the GPO to the production environment and links the GPO to an organizational unit (OU). |
| **Windows Firewall** | During installation, AGPM enables an inbound Windows Firewall rule that allows the AGPM client to communicate with the AGPM server. The default Windows Firewall rule has the following settings: <ul><li>**Name:** AGPM service</li><li>**Action:** Allow the connection</li><li>**Programs:** All programs that meet the specified conditions</li><li>**Protocol type:** TCP</li><li>**Local port:** 4600</li><li>**Remote port:** All ports</li><li>**Local IP address:** Any</li><li>**Remote IP address:** Any</li></ul> |
| **E-mail server** | AGPM uses Simple Mail Transfer Protocol (SMTP) to send e-mail requests to the addresses configured on the **Domain Delegation** tab. For example, when an editor requests that a new GPO be created, AGPM notifies each e-mail address specified on the **Domain Delegation** tab. |
| **AGPM snap-in** | The AGPM snap-in for the GPMC runs on AGPM clients and is used by group policy administrators to manage GPOs. The snap-in appears in the GPMC as a **Change Control** folder in each domain. |

## Archive

By default, the AGPM server installation process creates the archive on the local hard disk of the AGPM server at %ProgramData%\\Microsoft\\AGPM. However, you can change the path during installation and even create the archive on a server other than the AGPM server.

The archive contains a subfolder for each version of each GPO the archive contains. The name of each subfolder is a GUID that identifies a version of the GPO.

The gpostate.xml file records the state of each GPO in the archive. The file is a manifest that describes the contents of the archive. For example, a GPO can have many versions, and each version is in its own subfolder in the archive. The gpostate.xml file indicates which subfolders contain different versions of a single GPO. Additionally, GPO templates have subfolders in the archive, but gpostate.xml indicates that these items are templates and not controlled GPOs. Similarly, when group policy administrators delete GPOs, AGPM changes their states in gpostate.xml to indicate that they are in the **Recycle Bin** but doesn't actually remove the GPOs' subfolders from the archive.

> [!CAUTION]
> Don't manually edit gpostate.xml or the GPOs the archive contains. This information is provided only to enhance understanding of the AGPM archive. Instead, use the AGPM snap-in to change GPOs.

When AGPM creates the archive, it gives full control to SYSTEM, administrators, and the AGPM service account, which you specify in the setup of AGPM server. Changing permissions by using the AGPM user interface on the AGPM snap-in doesn't alter permissions on the archive, because the AGPM service Account performs all operations on behalf of the signed-in user.

For more information about how to back up the archive, restore the archive from a backup, or move both the AGPM server and the archive, see [Performing AGPM administrator tasks guidance](performing-agpm-administrator-tasks-agpm40.md).

## Roles and permissions

Roles simplify delegation. Instead of assigning detailed permissions to group policy administrators, AGPM administrators can assign one of four roles to group policy administrators to let them perform work related to that role:

- **AGPM administrator:** Group policy administrators assigned the AGPM administrator (full control) role can perform any task in AGPM. AGPM administrators can configure domain-wide options and delegate permissions to other group policy administrators.

- **Approver:** Group policy administrators assigned the approver role can deploy GPOs to the production environment for a domain. Approvers can also create and delete GPOs and approve or reject requests from editors. Approvers can view the list of GPOs in a domain, view the policy settings in GPOs, and create and view reports of the policy settings in a GPO. They can't edit the policy settings in GPOs unless they're also assigned the editor role.

- **Editor:** Group policy administrators assigned the editor role can view the list of GPOs in a domain, view the policy settings in GPOs, edit the policy settings in GPOs, and create and view reports of the policy settings in a GPO. Unless they're also assigned the approver role, editors can't create, deploy, or delete GPOs. However, they can request that GPOs are created, deployed, or deleted.

- **Reviewer:** Group policy administrators assigned the reviewer role can view the list of GPOs in a domain and create and view reports of the policy settings in a GPO. Unless they're also assigned the editor role, they can't edit policy settings in a GPO.

AGPM gives AGPM administrators the flexibility to configure permissions at a more detailed level than roles by using the AGPM snap-in. Table 2 describes these permissions and indicates the permissions granted to each role by default.

| Permission | Description | AGPM administrator | Approver | Editor | Reviewer |
|--|--|--|--|--|--|
| **Full Control** | Have all permissions. | Yes |  |  |  |
| **Create GPO** | Create GPOs in a domain. | Yes | Yes |  |  |
| **List Contents** | List the GPOs in a domain. | Yes | Yes | Yes | Yes |
| **Read Settings** | Read the policy settings within a GPO. | Yes | Yes | Yes | Yes |
| **Edit Settings** | Change the policy settings in a GPO. | Yes |  | Yes |  |
| **Delete GPO** | Delete a GPO. | Yes | Yes |  |  |
| **Modify Security** | Delegate domain-level access, delegate access to a single GPO, and delegate access to the production environment. | Yes |  |  |  |
| **Deploy GPO** | Deploy a GPO from the archive to the production environment. | Yes | Yes |  |  |
| **Create Template** | Create a GPO template in AGPM. | Yes |  | Yes |  |
| **Modify Options** | Configure AGPM e-mail notification and limit the GPO versions stored in the archive. | Yes |  |  |  |
| **Export GPO** | Export a GPO to a file. | Yes |  | Yes |  |
| **Import GPO** | Import a GPO from a file. | Yes |  | Yes |  |

## Related articles

For more information, see [Operations guide for Microsoft Advanced Group Policy Management 4.0](operations-guide-for-microsoft-advanced-group-policy-management-40.md).
