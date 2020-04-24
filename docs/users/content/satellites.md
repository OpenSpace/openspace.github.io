---
title: Satellites
layout: default

parent: Components
nav_order: 2
---

## How to add Satellites to OpenSpace
OpenSpace uses the `openspace.cfg` file for general configuration. With this file set to use the default.scene file (`Asset = "default"`), satellite categories can then be added by editing `data/assets/default.scene` and adding the following line (or un-comment it if already present):
`asset.request('scene/solarsystem/planets/earth/satellites/satellites')`
The satellites.asset file can include one or more satellite asset files. Open any of the satellites\_\*.asset files to see some of the different options available. These categories were created by CelesTrak.com, an online satellite tracking site from which these files are downloaded. In fact, the satellite data files (in TLE format) specified above are downloaded from celestrak.com every time OpenSpace runs. This is done in order to obtain the very latest telemetry.

## Running OpenSpace with Satellites
To start, double-click (or run from terminal) `bin/Release/OpenSpace.exe`. There will be a number of log messages for the individual satellites that appear while the scene is loading. Once loaded, Earth will be the camera's focus and the satellites and their orbital trails will be visible.
A list of all satellite groups can be viewed by selecting in the GUI: Scene -> Solar System -> Planets -> Earth -> Satellites. All satellite objects are grouped within the categories listed. The check box with each group can be used to toggle the visibility of all its satellites.
It is possible to modify the length of the orbital trail by adjusting the "Line fade" value in Renderable -> Appearance in the satellite group. A higher fade value shows more of the periodic orbital trails of the satellites.

## Additional Features
See the Components/Satellites [page](../../components/satellites.md) for more detailed information and advanced usage of satellites in OpenSpace.
