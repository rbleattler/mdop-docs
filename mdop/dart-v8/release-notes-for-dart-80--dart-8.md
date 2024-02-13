---
title: Release Notes for DaRT 8.0
description: Release Notes for DaRT 8.0
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.date: 08/30/2016
---

# Release Notes for DaRT 8.0

Read these release notes thoroughly before you install Microsoft Diagnostics and Recovery Toolset (DaRT) 8.0.

These release notes contain information that is required to successfully install DaRT 8.0. The release notes also contain information that isn't available in the product documentation. If there's a difference between these release notes and other DaRT documentation, the latest change should be considered authoritative. These release notes supersede the content that is included with this product.

## Known issues with DaRT 8.0

### System restore fails when you run Locksmith or Registry Editor

If you run Locksmith, Registry Editor, and possibly other tools, System Restore fails.

**Workaround:** Close and restart DaRT and then start System Restore.

### SFC scan fails to run after you launch and close Locksmith or Computer Management

If you start and then close the Locksmith or Computer Management tools, System File Checker fails to run.

**Workaround:** Close and restart DaRT and then start SFC.

### DaRT installer doesn't fail when ADK hasn't been installed

If you install DaRT 8.0 by using the command line to execute the MSI, and the ADK hasn't been installed, the DaRT installation should fail. Currently, the DaRT 8.0 installer installs all components except the DaRT 8.0 recovery image.

**Workaround:** None.

### Defender can't be launched after Locksmith, RegEdit, Crash Analyzer, and Computer Management are launched

Defender doesn't launch if you have already launched Locksmith, RegEdit, Crash Analyzer, and Computer Management.

**Workaround:** Close and restart DaRT and then launch Defender.

### Defender may be slow to launch

Defender sometimes takes a few minutes to launch. The progress bar indicates the current loading status.

**Workaround:** None.


## Related information

[About DaRT 8.0](about-dart-80-dart-8.md)
