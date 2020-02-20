---
title: Flexible Presentation
layout: default

grand_parent: Users
parent: Tutorials
nav_order: 1
---

# Overview
There are many ways that OpenSpace can be used to visualize space concepts, one of which is as an effective tool for presenting to an audience.  The presentation can range from an open-ended, ad-hoc discussion to a fixed script.  This tutorial describes the creation of a simple presentation that lies somewhere in the middle of this spectrum--not so unstructured that an audience might lose patience with the slow pace of a presenter who is "winging it," but not as inflexible as an educational film.  This technique is somewhat like a slideshow where the presenter can show things in segments, allowing for questions, comments, or even repeating segments if necessary. This allows for a more collaborative session with the audience.

OpenSpace provides a high degree of visibility and control to its internal states through a Lua script interface.  Specific Lua commands can be used to set internal property values in order to execute each step.  Each command described here could be executed in the Lua console (accessible by pressing \`), or through the GUI menu.  However, either method would be time-consuming and distracting during a presentation. The commands can instead be assigned to specific keyboard presses.

# Presentation
This tutorial describes how to configure OpenSpace to visualize the 2017 solar eclipse as its shadow moves across North America, and also the position of the moon relative to the sun.  The presenter starts OpenSpace with a focus on Earth.  Pressing F5 brings the camera view to center on North America at an appropriate altitude to view the shadow's path.  Pressing F6 changes the simulation time to August 21, 2017 16:45 UTC. After discussing some of the details, the presenter presses F7 to speed up the rate of simulation time to 5 minutes per second, in order to show the shadow moving across the continent.  The rate of time acceleration makes the movement fast enough to see, while giving the presenter time to discuss the eclipse in more detail.  When the shadow has passed, F8 is pressed to bring the time rate back to 1 sec/sec.  Finally, F9 is pressed to center the camera view on the Moon to show its path across the sun relative to Earth's position.

# Configuring OpenSpace for the Presentation
## Create New Configuration & Scene Files
At startup, OpenSpace uses a .cfg file to tell it how to configure the display, what scene will be loaded, and many other settings.  The default config file is **openspace.cfg**.  Create a copy of this file and rename it **eclipse2017.cfg**.  Open this file in a text editor, and scroll down to find where the variable `Asset` is defined.  The comment header above it explains that this sets the scene to be loaded by OpenSpace (ignore the other Asset lines which are disabled by the Lua comment header `--`).  The `Asset` variable is normally set to "default", which is the name of a file in the directory **data/assets/** (the **.scene** file extension is assumed but not listed here).  Change this assignment to `Asset = presentations/eclipse2017`, which tells OpenSpace to load the scene file **data/assets/presentations/eclipse2017.scene**.  Now create this scene file by creating a new directory in **data/assets** called **presentations**.  Copy the file **data/assets/default.scene** to this new directory and rename it **eclipse2017.scene**.  Finally, open this new **data/assets/eclipse2017.scene** file in a text editor, and add a `../` prefix to each `asset.require` and `asset.request` statement it contains.  For example, all such statements will be changed from this:
`asset.require('spice/base')`
to this:
`asset.require('../spice/base')`

## Assigning Keyboard Shortcuts
Now open **eclipse2017.scene** in a text editor and add the details necessary to set up actions for each keypress described above.  There is a Lua entry for `Keybindings` near the top of the file, with an individual entry for each key.  Add the following text to the `Keybindings` section (inside curly braces).
```
    {
        Key = "F5",
        Name="Eclipse: Set position North America",
        Command = "openspace.globebrowsing.goToGeo(40, -98, 5000000)",
        Documentation = "Sets position over North America for eclipse path to be visible",
        GuiPath = "/Rendering",
        Local = false
    },
    {
        Key = "F6",
        Name="Eclipse: Set to date & time",
        Command = "openspace.time.setTime(\"2017 AUG 21 16:45:00\")",
        Documentation = "Sets date & time to when eclipse begins movement over North America",
        GuiPath = "/Rendering",
        Local = false
    },
    {
        Key = "F7",
        Name="Eclipse: Set to accelerated time",
        Command = "openspace.time.interpolateDeltaTime(300)",
        Documentation = "Sets simulated time rate to 5 minutes per second to show shadow movement",
        GuiPath = "/Rendering",
        Local = false
    },
    {
        Key = "F8",
        Name="Eclipse: Set to accelerated time",
        Command = "openspace.time.interpolateDeltaTime(1)",
        Documentation = "Sets simulated time rate back to normal 1 sec per sec",
        GuiPath = "/Rendering",
        Local = false
    },
    {
        Key = "F9",
        Name="Eclipse: Set moon as focus node",
        Command = "openspace.setPropertyValue('NavigationHandler.Origin', 'Moon')",
        Documentation = "Sets camera view to moon in order to show Earth/moon/sun relative positions",
        GuiPath = "/Rendering",
        Local = false
    },

```
Each entry specifies the key, and has a name and documentation entry with it.  The `Command` string is the Lua command that executes the desired action.  When finished, save and close the file.
Details of these and many other commands can be found in the documentation/ directory in the OpenSpace installation.  The `.html` files located there can be opened in a web browser.  **KeyboardMapping.html** lists the default key bindings that OpenSpace uses, and files like **LuaScripting.html** and **SceneProperties.html** provide a great amount of information.  These documents are to be used as references, and since they are auto-generated, they supersede any details or syntax in this or other documents.

## Starting OpenSpace to Display This Scene
Now it is time to run OpenSpace with this presentation scene.  Open a terminal and navigate to the base OpenSpace directory.  Enter the path to the executable, and specify using the newly-created **eclipse2017.cfg** file (OpenSpace defaults to using **openspace.cfg** if none is specified).  The commands should look something like this Windows example:
```
cd C:\directory\to\OpenSpace
bin\OpenSpace.exe -f eclipse2017.cfg
```
OpenSpace will start with Earth as the camera focus, and the presenter can then go through the steps described above at his/her own pace.

# Using this Technique for Camera Playback using "Session Recording"
This is an example of a simple scene, but these techniques can be used to create a presentation with much more detail.  Session Recording is another OpenSpace feature that is useful for presenting (covered in a separate document [here](http://wiki.openspaceproject.com/components/session-recording-playback/general)).  This feature can record all of the specific details and precise camera movements that a presenter might want to show an audience.  Camera movements can be saved in individual files, and then played back in discrete steps using keybindings in order to provide a more free-form presentation like the collaborative format described above.

This idea was implemented for a presentation, and configured to work with a single keypress.  When a playback segment ends, the presenter can talk about the scene, and then press the Backspace key to start the next playback segment when desired.  To do this, the following section was added to the `Keybindings` section of the .scene file.  This segment of code would be pasted in the same section as the example given above.
```
   {
        Key = "BACKSPACE",
        Name="Advance to next playback",
        Command = 
          [[if slideNum == 0 then
            openspace.sessionRecording.startPlayback('C:/openspace/recordings/playback_00.dat')
          elseif slideNum == 1 then
            openspace.sessionRecording.startPlayback('C:/openspace/recordings/playback_01.dat')
          elseif slideNum == 2 then
            openspace.sessionRecording.startPlayback('C:/openspace/recordings/playback_02.dat')
          end
          slideNum = slideNum + 1                           
          ]],
        Documentation = "Advances to the next playback segment in a presentation",
        GuiPath = "/Rendering",
        Local = false
    },
```
After adding this to the `Keybindings` section, add the variable definition `slideNum = 0` as a single line immediately above that section.
