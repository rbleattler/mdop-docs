---
title: Create, edit, and deploy a GPO checklist
description: In an environment where multiple people change group policy objects (GPOs) by using Advanced Group Policy Management (AGPM), an AGPM administrator (full control) delegates permission to editors, approvers, and reviewers either as groups or as individuals.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Create, edit, and deploy a GPO checklist

In an environment where multiple people change group policy objects (GPOs) by using Advanced Group Policy Management (AGPM), an AGPM administrator (full control) delegates permission to editors, approvers, and reviewers either as groups or as individuals. The following table lists a typical GPO development process for an editor and an approver.

| Task | Reference |
|--|--|
| An editor requests that a new GPO is created or an approver creates a new GPO. | [Request the creation of a new controlled GPO](request-the-creation-of-a-new-controlled-gpo-agpm40.md) <br> [Create a new controlled GPO](create-a-new-controlled-gpo-agpm40.md) |
| An editor requests the creation of a GPO, and an approver approves it. | [Approve or reject a pending action](approve-or-reject-a-pending-action-agpm40.md) |
| An editor checks out a copy of the GPO from the archive so that no one else can modify the GPO. The editor makes changes to the GPO, and then checks the modified GPO into the archive. | [Edit a GPO offline](edit-a-gpo-offline-agpm40.md) |
| If developing in a test forest, an editor exports the GPO to a file. They then transfer the file to the production forest, and import the file. Additionally, an editor can link the GPO to an organizational unit (OU) that contains test computers and users. | [Using a test environment](using-a-test-environment.md) |
| An editor requests deployment of the GPO to the production environment of the domain. | [Request deployment of a GPO](request-deployment-of-a-gpo-agpm40.md) |
| Reviewers, such as approvers or editors, analyze the GPO. | [Performing reviewer tasks](performing-reviewer-tasks-agpm40.md) |
| An approver approves and deploys the GPO to the production environment of the domain or rejects the GPO. | [Approve or reject a pending action](approve-or-reject-a-pending-action-agpm40.md) |
