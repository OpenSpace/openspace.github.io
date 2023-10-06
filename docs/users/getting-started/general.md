---
title: Getting Started Guide
layout: default

parent: Users
has_children: true
has_toc: false
nav_order: 1
---

The best-supported platform for running OpenSpace is a Windows 10 machine with at least 8GB RAM and a discrete graphics card (Nvidia cards work best, but AMD cards work with some issues). For minimum requirements by profile, see [Hardware Requirements](/docs/users/getting-started/hardware-requirements.html).

Ensure to complete the steps found in the [Download, Install and Run](http://wiki.openspaceproject.com/docs/tutorials/users/downloadinstall.html) section prior to proceeding. **The video provides especially critical configuration instructions to ensure the software properly runs.**

Once you get OpenSpace to build, or have installed it from a .zip file, it's time to run it. The OpenSpace executable can be found in the `bin/` directory (or in `bin/Release` or `bin/RelWithDebInfo` if compiled on windows).
Here is a brief overview of what you need to know to get started.

## Initial Sync
The data used by OpenSpace includes a number of very large data files, which cannot be stored on GitHub.  The first time you fire up a fresh build or a new install of OpenSpace you need to "Sync" it to download some or all of these data files.  The first time you run either executable it will also create several additional subdirectories, including subdirectories called `cache` and `documentation`.

To perform the Sync you just start OpenSpace with the scene and and wait several minutes.

### Navigation Via Mouse
Navigation in OpenSpace is based on the central object of the Scene, which is called the "Origin" or "Focus".  You can change your viewpoint around the origin using mouse motion. You must press and hold a button (or a combination of buttons) while you move the mouse.
- Left mouse button - rotate position around the origin
- Middle mouse button - roll
- Right mouse button - zoom in or out (by moving the mouse forward or backward)
- CTRL+left mouse - pitch and yaw camera direction away from the origin

More info on how to navigate in the software can be found under "Navigation" in the menu to the left on this page, or in the video tutorials under "User Tutorials". For basic navigation, see [this page](/docs/users/navigation/basic-navigation.html). In addition, use the "Open Getting Started Tour" feature in the side menu (3 vertical dots next to Scene command) when using OpenSpace to practice the Navigation controls.

### Keyboard Commands
The first section of [this wiki page](../commandline) explains how to use the console for entering commands. After starting a scene, the `documentation/KeyboardMapping.html` file will contain a list of all keyboard bindings that are valid for the current scene.

## Configuration Files
All main configuration starts with the file `openspace.cfg` in the main  OpenSpace folder.  This file is read first upon startup, and it references two other configuration files, identified by the `SGCTConfig` and `Asset` keys.
