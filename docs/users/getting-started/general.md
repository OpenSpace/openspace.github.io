---
title: Getting Started Guide
layout: default

parent: Users
has_children: true
has_toc: false
nav_order: 1
---

Once you get OpenSpace to build, or have installed it from a .zip file, it's time to run it. The OpenSpace executable can be found in the `bin/` directory (or in `bin/Release` or `bin/RelWithDebInfo` if compiled on windows).
Here is a brief overview of what you need to know to get started.

## Initial Sync
The data used by OpenSpace includes a number of very large data files, which cannot be stored on GitHub.  The first time you fire up a fresh build or a new install of OpenSpace you need to "Sync" it to download some or all of these data files.  The first time you run either executable it will also create several additional subdirectories, including subdirectories called `cache` and `documentation`.

1. To perform the Sync you just start OpenSpace with the scene and and wait

### Navigation via mouse
Navigation in OpenSpace is based on the central object of the Scene, which is called called the "Origin".  You can change your viewpoint around the origin using mouse motion.   You must press and hold a button (or combination of buttons) while you move the mouse.
- Left mouse button - rotate position around the origin
- Middle mouse button - roll
- Right mouse button - zoom in or out (by moving the mouse forward or backwards)
- CTRL+left mouse - pitch and yaw camera direction away from the origin

### Editing Internal Settings
Press the `F1` brings up a menu of possible internal OpenSpace settings.  These will be documented on a separate page.  For now, two of the items you may be interested in are setting the `Origin` (the central object in the Scene) and the `Delta Time`, which controls how fast time passes in the simulation relative to real-world time.  The menu for the `Origin` is a scroll-down menu.  For `Delta Time` you can either slide the mouse across the field to change the value like a slider, or type a numerical value.

When a submenu is open, you'll find the close button in the upper right corner.  It looks like a circle, but it will become an "X" when the mouse pointer moves over it.  Click the "X" to close the submenu.

The main menu is closed by pressing `F1` again

### Keyboard Commands
The first section of [this wiki page](../commandline) explains how to use the console for entering commands. After starting a scene, the `documentation/KeyboardMapping.html` file will contain a list of all keyboard bindings that are valid for the current scene.

## Configuration Files
All main configuration starts with the file `openspace.cfg` in the main  OpenSpace folder.  This file is read first upon startup, and it references two other configuration files, identified by the `SGCTConfig` and `Asset` keys.
