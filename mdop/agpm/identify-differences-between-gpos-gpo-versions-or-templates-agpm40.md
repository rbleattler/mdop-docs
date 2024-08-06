---
title: Differences between GPOs, GPO versions, or templates
description: You can generate HTML-based or XML-based difference reports to analyze the differences between group policy objects (GPOs), templates, or different versions of a GPO.
author: aczechowski
ms.assetid: 3f03c368-162b-450f-be6c-2807c3e8d741
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.pagetype: mdop
ms.mktglfcycl: manage
ms.sitesec: library
ms.date: 06/16/2016
---


# Differences between GPOs, GPO versions, or templates

You can generate HTML-based or XML-based difference reports to analyze the differences between group policy objects (GPOs), templates, or different versions of a GPO.

A user account with the reviewer, editor, approver, or Advanced Group Policy Management (AGPM) administrator (full control) role or necessary permissions in AGPM is required to complete this procedure.

## To identify differences between two GPOs or templates

1.  In the **Group Policy Management Console** tree, select **Change Control** in the forest and domain in which you want to manage GPOs.

2.  On the **Contents** tab in the details pane, select a tab to display GPOs (or templates, if comparing two templates).

3.  Select the two GPOs or templates.

4.  Right-click one of the GPOs or templates, select **Differences**, and then select **HTML Report** or **XML Report** to display a difference report summarizing the settings of the GPOs or templates.

## To identify differences between a GPO and a template

1.  In the **Group Policy Management Console** tree, select **Change Control** in the forest and domain in which you want to manage GPOs.

2.  On the **Contents** tab in the details pane, select a tab to display GPOs (or templates, if comparing two templates).

3.  Right-click the GPO, select **Differences**, and then select **Template**.

4.  Select the template and type of report, and then select **OK** to display a difference report summarizing the settings of the GPO and template.

## To identify differences between two versions of one GPO

1.  In the **Group Policy Management Console** tree, select **Change Control** in the forest and domain in which you want to manage GPOs.

2.  On the **Contents** tab in the details pane, select a tab to display GPOs (or templates, if comparing two templates).

3.  Double-click the GPO to display its history, and then highlight the versions to be compared.

4.  Right-click one of the versions, select **Differences**, and then select **HTML Report** or **XML Report** to display a difference report summarizing the settings of the GPOs.

## To identify differences between a GPO version and a template

1.  In the **Group Policy Management Console** tree, select **Change Control** in the forest and domain in which you want to manage GPOs.

2.  On the **Contents** tab in the details pane, select a tab to display GPOs (or templates, if comparing two templates).

3.  Double-click the GPO to display its history.

4.  Right-click the GPO version of interest, select **Differences**, and then select **Template**.

5.  Select the template and type of report, and then select **OK** to display a difference report summarizing the settings of the GPO version and template.

## Key to difference reports

| Symbol | Meaning | Color |
|--|--|--|
| None | Item exists with identical settings in both GPOs | Varies with level |
| `#` | Item exists in both GPOs, but with changed settings | Blue |
| `-` | Item exists only in the first GPO | Red |
| `+` | Item exists only in the second GPO | Green |

- For items with changed settings, the changed settings are identified when the item is expanded. The value for the attribute in each GPO is displayed in the same order that the GPOs are displayed in the report.

- Some changes to settings might cause an item to be reported as two different items (one present only in the first GPO, one present only in the second) rather than as one item that has changed.

## Other considerations

By default, you must be a reviewer, an editor, an approver, or an AGPM administrator (full control) to do this procedure. Specifically, you must have **List Contents** and **Read Settings** permissions for the GPO. Also, to display the list of GPOs, you must have **List Contents** permission for the domain.

### Other articles

- [Performing Reviewer Tasks](performing-reviewer-tasks-agpm40.md)
