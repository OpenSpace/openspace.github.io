---
title: Flexible Presentation
layout: default

grand_parent: Users
parent: Tutorials
nav_order: 1
---

# Overview
There are many ways that OpenSpace can be used to visualize space concepts, one of which is as an effective tool for presenting to an audience. The presentation can range from an open-ended, ad-hoc discussion to a fixed script. This tutorial describes the creation of a simple presentation that lies somewhere in the middle of this spectrum--not so unstructured that an audience might lose patience with the slow pace of a presenter who is "winging it," but not as inflexible as an educational film. This technique is somewhat like a slideshow where the presenter can show things in segments, allowing for questions, comments, or even repeating segments if necessary. This allows for a more collaborative session with the audience.

OpenSpace provides a high degree of visibility and control to its internal states through a Lua script interface. Specific Lua commands can be used to set internal property values in order to execute each step. Each command described here could be executed in the Lua console (accessible by pressing \`), or through the GUI menu. However, either method would be time-consuming and distracting during a presentation. The commands can instead be assigned to specific keyboard presses.

# Presentation
This tutorial describes how to configure OpenSpace to visualize a flyover of Mars. The presenter starts OpenSpace with a focus on Earth. Pressing the right arrow initiates a flight to Mars, and subsequent right arrows will initiate other movements to different locations on Mars.

# Configuring OpenSpace for the Presentation
## Create New Configuration & Profile Files
At startup, OpenSpace uses a .cfg file to tell it how to configure the display, what scene will be loaded, and many other settings. The default config file is **openspace.cfg**, and will have an un-commented (`--`) line to load the default profile (`Profile = "default"`). Copy this line and paste below it, modifying it to instead read `Profile = "mars_flight"`). Finally, comment-out the original default Profile line.

Now create this new **mars_flight.profile** file by going to **data/profiles/** in a file browser, copy **default.profile** and rename the new file **mars_flight.profile**.
Open **mars_flight.profile** in a text editor, and replace the contents with the following:
```
#Version
1.0

#Asset
base   
scene/solarsystem/planets/earth/earth    earthAsset
addons/testflight

#Property
setPropertyValue    {earth_satellites}.Renderable.Enabled    false
setPropertyValue    "NavigationHandler.OrbitalNavigator.RetargetAnchorInterpolationTime"    2.000000
setPropertyValue    "Scene.Mars.Renderable.Layers.ColorLayers.CTX_belended_01.Enabled"    true
setPropertyValue    "Scene.Mars.Renderable.Layers.ColorLayers.CTX_belended_01.Settings.Opacity" 0.0
setPropertyValue    "Scene.Mars.Renderable.Layers.ColorLayers.Southwest_Candor_Chasma.Enabled"    true
setPropertyValue    "Scene.Mars.Renderable.Layers.HeightLayers.Southwest_Candor_Chasma.Enabled"    true

#Time
relative    -1d

#Camera
goToGeo    earthAsset.Earth.Identifier    58.5877    16.1924    40000000

#MarkNodes
Earth
Mars
Moon
Sun

#AdditionalScripts
openspace.globebrowsing.addFocusNodeFromLatLong("Olympus Mons", "Mars", 18.65, 226.2, 1000)
openspace.globebrowsing.addFocusNodeFromLatLong("Western Candor", "Mars", -6.48, -76.92, 1000)
```

## Add Asset File That Contains the Individual Navigation Steps
First create a new **addons/** directory in the **data/assets/** OpenSpace file path, and then add a new **testflight.asset** file there (the full path will be **data/assets/addons/testflight.asset**). Add the following contents to the file, and save it.
```
local stateMachineHelper = asset.require('util/state_machine_helper')

local states = {
    {
        Title = "Start",
        Play = function ()
            openspace.printInfo("Start focused on Earth")
            openspace.globebrowsing.goToGeo("Earth", 58.5877, 16.1924, 20000000)
        end,
        Rewind = function ()
        end
    },
    {
        Title = "LookAtMars",
        Play = function ()
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.Aim", '')
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.Anchor", 'Mars')
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.RetargetAnchor", nil)
            openspace.printInfo("Look at Mars")
        end,
        Rewind = function ()
        end
    },
    {
        Title = "FlytoMars",
        Play = function ()
            openspace.setPropertyValueSingle("Scene.Mars.Renderable.Layers.ColorLayers.Southwest_Candor_Chasma.Settings.Opacity", 0.0)
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.VelocityZoomControl", .01 )
            openspace.setPropertyValueSingle('NavigationHandler.OrbitalNavigator.FlightDestinationDistance', 20000000.0)
            openspace.setPropertyValue('NavigationHandler.OrbitalNavigator.ApplyLinearFlight', true)
            openspace.printInfo("Going to Mars")
        end,
        Rewind = function ()
        end
    },
    {
        Title = "Aim On Olympus Mons",
        Play = function ()
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.Aim", 'Mars-Olympus Mons')
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.RetargetAim", nil)
            openspace.printInfo("Going to Olympus Mons")
        end,
        Rewind = function ()
        end
    },
    {
        Title = "Anchor On Olympus Mons and zoom down",
        Play = function ()
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.VelocityZoomControl", .005 )
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.Anchor", 'Mars-Olympus Mons')
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.RetargetAnchor", nil)
            openspace.setPropertyValueSingle('NavigationHandler.OrbitalNavigator.FlightDestinationDistance', 300000.0)
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.ApplyLinearFlight", true)
            openspace.setPropertyValueSingle("Scene.Mars.Renderable.Layers.ColorLayers.CTX_belended_01.Settings.Opacity", 1.0,10)
            openspace.printInfo("Anchor On Olumpus Mons and Zoom Down")
        end,
        Rewind = function ()
        end
    },
    {
        Title = "LiftUp",
        Play = function ()
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.RetargetAnchorInterpolationTime", 10.000000)
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.Anchor", 'Mars')
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.Aim", 'Mars')
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.RetargetAnchor", nil)
            openspace.setPropertyValueSingle("Scene.Mars.Renderable.Layers.ColorLayers.CTX_belended_01.Settings.Opacity", 0.0,1)
            openspace.setPropertyValueSingle('NavigationHandler.OrbitalNavigator.FlightDestinationDistance', 4000000.0)
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.ApplyLinearFlight", true)
            openspace.printInfo("Lift Up")
        end,
        Rewind = function ()
        end
    },
    {
        Title = "Aim On Candor Chasma",
        Play = function ()
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.Aim", 'Mars-Western Candor')
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.RetargetAim", nil)
            openspace.printInfo("Aiming Candor Chasma")
        end,
        Rewind = function ()
        end
    },
    {
        Title = "Anchor On Candor Chasma and zoom down",
        Play = function ()
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.Anchor", 'Mars-Western Candor')
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.RetargetAnchor", nil)
            openspace.setPropertyValueSingle('NavigationHandler.OrbitalNavigator.FlightDestinationDistance', 10000.0)
            openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.ApplyLinearFlight", true)
            openspace.setPropertyValueSingle("Scene.Mars.Renderable.Layers.ColorLayers.CTX_belended_01.Settings.Opacity", 1.0,10)
            openspace.setPropertyValueSingle("Scene.Mars.Renderable.Layers.ColorLayers.Southwest_Candor_Chasma.Settings.Opacity",1.0,10)
            openspace.printInfo("Zoom Down on Candor Chasma")
        end,
        Rewind = function ()
        end
    }
}

local stateMachine

function next()
    stateMachine.goToNextState()
end

function previous()
    stateMachine.goToPreviousState()
end



asset.onInitialize(function ()
    stateMachine = stateMachineHelper.createStateMachine(states)
    openspace.bindKey('RIGHT', 'next()')
    openspace.bindKey('LEFT', 'previous()')
end)


asset.onDeinitialize(function ()
    stateMachine = nil
    openspace.clearKey('RIGHT')
    openspace.clearKey('LEFT')
end)
```

Each sub-entry under `states` defines a navigation step that can be individually triggered by pressing the right arrow.

## Starting OpenSpace to Display This Scene
Now it is time to run OpenSpace with this presentation scene.  With the **openspace.cfg** file as described above, double-clicking the OpenSpace icon will run with this new profile.

# Using this Technique for Camera Playback using "Session Recording"
This is an example of a simple scene, but these techniques can be used to create a presentation with much more detail.  Session Recording is another OpenSpace feature that is useful for presenting (covered in a separate document [here](http://wiki.openspaceproject.com/docs/components/session-recording)).  This feature can record all of the specific details and precise camera movements that a presenter might want to show an audience.  Camera movements can be saved in individual files, and then played back in discrete steps using keybindings in order to provide a more free-form presentation like the collaborative format described above.

To use session recording/playback files, the `openspace.setPropertyValueSingle("NavigationHandler.OrbitalNavigator.*")` commands in the above example could be replaced with a command `openspace.sessionRecording.startPlayback('playback_00.dat')` where **playback_00.dat** is a previously-recorded file in the **recordings/** directory. Additional playback files can of course be added.
