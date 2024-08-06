---
title: Search and filter the list of GPOs
description: In Advanced Group Policy Management (AGPM), you can search the list of group policy objects (GPOs) and their attributes to filter the list of GPOs displayed.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Search and filter the list of GPOs


In Advanced Group Policy Management (AGPM), you can search the list of group policy objects (GPOs) and their attributes to filter the list of GPOs displayed. For example, you can search for GPOs with a particular name, state, or comment. You can also search for GPOs that were last changed by a particular group policy administrator or on a particular date.

## Complex search

You can do a complex search by using the format *GPO attribute 1: search string 1 GPO attribute 2: search string 2…all-column search strings*. The search isn't case-sensitive.

- **GPO attribute:** Any column heading in the list of GPOs in AGPM other than **Computer Version** or **User Version**. GPO attributes include the GPO name, state, user who most recently changed the GPO, date, and time when the GPO was most recently changed, comment, GPO status, and WMI filter applied to the GPO.

- **Search string:** Text for which to search in the specified column. If a string includes spaces, you must enclose the string with quotation marks.

- **All-column search strings:** Text for which to search in all columns in the list of GPOs in AGPM other than **Computer Version** and **User Version**. You can include multiple strings separated by spaces. If a string includes spaces, you must enclose the string with quotation marks.

Each GPO attribute and search string pair and each all-column search string are combined by using a logical AND operation. The result is a list of all GPOs for which each specified attribute includes the specified search string and for which any all-column search strings appear in at least one column. The search returns any partial matches for strings so that you can enter part of a GPO name or user name and view a list of all GPOs that include that text in their name.

The following are examples of searches:

| Description of search result | Search query |
|--|--|
| All GPOs with names that include the text **security** and **North America**. | **name:** **security** **name:** " **North America** " |
| All checked out GPOs. | **state:** " **checked out** " |
| All GPOs most recently changed by the user named **Administrator** and most recently changed within the previous month. | **changed by:** **Administrator** **change date:** **lastmonth** |
| All GPOs in which the word **firewall** is included in the most recent comment and in which the word **security** appears in any column. | **comment:** **firewall** **security** |
| All GPOs that have a status of **All Settings Disabled**. | **gpo status:** **all** |
| All GPOs that have a WMI filter named **My WMI Filter** applied and that have a status of **User Configuration Settings Disabled**. | **wmi filter:** " **My WMI Filter** " **gpo status:** **user** |

## Specifying dates

You can search for GPOs changed on a specific date, at a specific time, or during a span of time by using the same special terms available when you search in Windows. If entering a specific date or time, you must use the format that is used in the **Change Date** column. The following are examples of searches of the **Change Date** column:

- **change date:** **10/10/2009**

- **change date:** **10/10/2009 9:00:00 AM**

- **change date:** **thisweek**

You can use the following special terms, which aren't case-sensitive, when you search the **Change Date** column:

- **Today**

- **Yesterday**

- **ThisWeek**

- **LastWeek**

- **ThisMonth**

- **LastMonth**

- **TwoMonths**

- **ThreeMonths**

- **ThisYear**

- **LastYear**

### Other considerations

- By default, you must be a reviewer, an editor, an approver, or an AGPM administrator (full control) to perform this procedure. Specifically, you must have **List Contents** permission for the domain.

- For more information about GPO attributes, see [Contents tab features](contents-tab-features-agpm40.md).
