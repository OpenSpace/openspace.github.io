---
title: Satellites
layout: default

parent: Components
nav_order: 2
---

This module was created to visualize satellites in earth orbit.  The precise position of each satellite above the Earth is rendered according to the date & time.  The Two-Line Element set (TLE) file format is a standard for defining satellite orbital mechanics.  It contains all of the necessary Keplerian elements to define an orbital path.  When running the satellites module, OpenSpace reads all of the provided TLE files and generates a renderable for each entry.

## How to Run the Satellites Module
OpenSpace uses the `openspace.cfg` file for general configuration.  Among this file's variables is `Asset`, which defines the base asset (formerly scene) to use for rendering: `Asset = "default"`.  To include satellites visualization in the default asset, open `data/assets/default.scene` and add the following line (or un-comment it if already present):
`asset.request('scene/solarsystem/planets/earth/satellites/satellites')`

Double-click `bin/Release/OpenSpace.exe` to run using the openspace.cfg configuration, or run from a terminal.  There will be a number of log messages for the individual satellites that appear while the scene is loading.  Once loaded, Earth will be the camera's focus and the satellites and their orbital trails will be visible.
A comprehensive list of all satellites can be viewed by pressing _F2_ and then in the "Properties" browser select Solar System -> Planets -> Earth -> Satellites, which will provide a list for each renderable.  All satellite renderables have a name that begins with the file containing its TLE file entry.  For example, if a satellite's TLE information is contained in the file `stations.txt`, then its renderable name will have a `stations_` prefix.  Each satellite will also have a trail renderable, with a `_trail` suffix in the name.  Rendering controls for each satellite are available in the dialog box, including enabling/disabling visibility, color control, etc.
From the OpenSpace GUI dialog box (press _F2_) it is possible to change the camera's origin from Earth to any of the satellites in the list.

## Automation
OpenSpace features like regular expressions and keyboard bindings can be used to automate control of satellite layers.  Keyboard bindings can be added to an individual scene.  For example, in the `preInitialization` function of the file `default.scene`, the following `bindkey` command can be added:
```
    openspace.bindKey("p", "openspace.setPropertyValue(
                    'stations_*.renderable.Enabled', false)",
                    "Disable stations visibility")
```
The **\*** wildcard will apply the command to all renderables that meet the `stations_*` criteria in this case.  Regular expression syntax can also be used. When running OpenSpace, press _p_ to make all station satellites invisible.  Specific commands can also be entered in the terminal at runtime, without pre-configuring a scene file.  Press **\`** to get a terminal at the top of the window, and type: `openspace.setPropertyValue('stations_*.renderable.Enabled', true)`, and then all satellites from the `stations.txt` TLE file will become visible again.

## Customizing the Satellites Module
When OpenSpace starts the satellites module, it tries to download `.tle` files that are specified in the `data/assets/scene/solarsystem/planets/earth/satellites/satellites.asset` file.  At the top of this file, `satelliteGroups` contains a dictionary entry for each .tle file to be included in the visualization.  Each file has a `title` for its description, a `url` for where to download the latest .tle file, and a `trailColor`.  Further down in this file, the `UrlSynchronization` type is used to tell OpenSpace to download a copy from the URL specified (this is done for best orbital accuracy, since some satellite positions are updated often).  After downloading, OpenSpace will open each file and read all of the satellite entries that it contains (two lines for each satellite TLE entry).  For each TLE entry, OpenSpace computes the current orbital position and generates a renderable object.  If a large number of satellites are listed, then the initialization time as well as the rendering performance may be negatively impacted.
The default renderable image for each satellite is a simple white circle `satB.png` which is obtained from the server using the identifier `tle_satellites_images`.  Another image file can be substituted for this if desired.
