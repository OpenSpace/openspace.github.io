---
title: Releases
layout: default

parent: Home
nav_order: 1
---

# Releases
OpenSpace versions labeled by a version number of the form `MM.mm.rr`,  where `MM` is the major version number, `mm` is the minor version number, and `rr` is the release number (see [Semantic Versioning](https://semver.org)).  In some cases there may be an additional number at the end, `MM.mm.rr.bb`, where bb is the build number, but that will only be for development and testing, not for public release.

1. TOC
{:toc}

# Overview
As development proceeds, some versions get tagged with names.  This table indicates which version numbers go with which tags, and some notes about each:

| Version | _Name_ | _Date_ | _Description_ |
| ------- | ------ | ------ | - |
| 0.18.2 | Beta-11 | 2022-12-24 | This is a second patch release for the eleventh beta release | 
| 0.18.1 | Beta-11 | 2022-11-22 | This is a patch release for the eleventh beta release |
| 0.18.0 | Beta-11 | 2022-05-06 | This is the eleventh beta release and the first in 2022 |
| 0.17.2 | Beta-10 | 2021-08-27 | This is a patch release for the tenth beta that addresses an issue with Earth terrain |
| 0.17.1 | Beta-10 | 2021-08-09 | This is a patch release for the tenth beta that addresses initial bug reports |
| 0.17.0 | Beta-10 | 2021-07-14 | This is the tenth beta release and the second in 2021 |
| 0.16.1 | Beta-9 | 2021-05-07 | This is the ninth beta release and the first in 2021 |
| 0.16.0 | Beta-8 | 2020-12-09 | This is the eigth beta release for the end of 2020 |
| 0.15.2 | Beta-7 | 2020-06-26 | This is the seventh beta release for OpenSpace for the summer of 2020 |
| 0.15.1 | Beta-6 | 2020-02-17 | This is the sixth beta release for OpenSpace in conjunction with the 4th annual developer's meeting |
| 0.15.0 | Beta-5 | 2019-09-17 | This is the fifth beta release for OpenSpace released on September, 17th, 2019 for the ASTC conference |
| 0.14.1 | Beta-4 | 2019-06-04 | This is the first patch release for the fourth beta |
| 0.14.0 | Beta-4 | 2019-05-20 | This is the fourth beta release for OpenSpace released on the 20th of May, 2019 |
| 0.13.0 | Beta-3 | 2018-11-05 | This is the third beta release for OpenSpace released on the 5th of November, 2018 |
| 0.12.0 | Beta-2 | 2018-07-11 | This is the second beta release for OpenSpace released on the 11th July 2018 in the aftermath of IPS in Toulouse, France. |
| 0.11.1 | Beta-1 | 2018-02-13 | This is a patch release for the beta-1 version released on January 1st, 2018. It mainly fixes bugs and issues that have come up for users with the beta-1 release of OpenSpace. |
| 0.11.0 | Beta-1 | 2018-01-01 | This is the first beta release for OpenSpace released on January 1st, 2018. It contains all of the previously released features + new content and feature updates. |
| 0.10.0 | Prerelease-15 | 2017-10-24 | This prerelease is a collection of features that have been developed since the last public prerelease version for release at the Association of Science – Technology Centers (ASTC) conference. |
| 0.9.0 | Prerelease-14 | 2017-07-21 | This prerelease is a collection of features that have been developed since the last public prerelease version. |
| 0.8.0 | Prerelease-13 | 2017-04-18 | Prerelease for the Earth Day 2017 |
| 0.7.0 | Prerelease-12 | 2016-02-19 | NAOJ presentation |
| 0.6.0 | Prerelease-11 | 2016-12-14 | AGU presentation |
| 0.5.0 | Prerelease-10 | 2016-09-25 | Norrköping's Kulturnatten presentation |
| 0.4.0 | Prerelease-9 | 2016-07-11 | This pre-release version was prepared for a meeting at the AMNH of the ISI User Network. |
| 0.3.4 | Prerelease-8 | 2016-06-22 | IPS exhibition |
| 0.3.3 | Prerelease-8 | 2016-06-07 | EuroVis presentation |
| 0.3.2 | Prerelease-8 | 2016-04-15 | CCMC Show |
| 0.3.1 | Prerelease-8 | 2016-03-03 | New Horizons Show |
| 0.3.0 | Prerelease-8 | 2015-07-16 | |
| 0.2.1 | Prerelease-7 | 2015-07-15 | New Horizons Show |
| 0.2.0 | Prerelease-7 | 2015-07-08 | This prerelease was published for a global, networked event in celebration of New Horizon’s closest approach to Pluto. |
| 0.1.0 | Prerelease-5 | 2015-05-14 | This prerelease was published for the Pluto-Palooza event held at the AMNH in New York. |

***

# Beta-11 (Patch-2) [0.18.2]
 - Version: 0.18.2
 - Date: 2022-12-24
 - Finished: [7b09d1a2288090e403ef79317309ee9f16b2c37a](https://github.com/OpenSpace/OpenSpace/commit/7b09d1a2288090e403ef79317309ee9f16b2c37a)

## Bugfixes
  - Fix to a problem that caused the Mars profile to not load correctly
  - Fix for an issue that made the some of the options of the configuration helper functions in the openspace.cfg file unusable (#2364)
  - Fix to an asset dependecy issue that prevent the JWST asset from being included outside the JWST profile (#2378)
  - Fix to an issue that would prevent the FOV slider from working in a rendering+GUI window setup
  - Fix to prevent invalid entries for actions and keybindings in the Profile Editor (#2362)
  - Fixed and issue where it was possible to interact with a joystick during a camera path or a session recording
  - Fix problem with the interaction sphere of scene graph nodes without renderables being unused (#2399)
  - Fix issue where the explicit bounding sphere was being ignored (#1899)
  - Fixed a typo in the documentation for the RenderableTimeVaryingSphere


# Beta-11 (Patch-1) [0.18.1]
 - Version: 0.18.1
 - Date: 2022-11-22
 - Finished: [0a6aa29b1b0c054fa59236b008749d1b98ebca9d](https://github.com/OpenSpace/OpenSpace/commit/0a6aa29b1b0c054fa59236b008749d1b98ebca9d)

## Fixes to existing assets
 - Use the new ESRI WorldImagery URL
 - Use the new CelesTrek URL for all satellites fixing an issue where satellites would no longer appear due to a change in the CelesTrek API (#2135, #2146)
 - Fix the Mars profile so that Perseverance and Insight do not land inside Mars anymore and stay there as well (#2049)
 - Update OsirisREx kernels to include a missing kernel file that would prevent the profile from loading correctly (#2177)
 - Reorganized the assets for the NASA Treks values to make it less likely to end up with too long file paths on Windows when installing OpenSpace in a nested folder (#2311)
 - Fixed issue with Show All Trails / Hide all Trails when executed in a profile that did not have `*trail` and `*Trail` scene graph nodes 
 - Updated the bounding spheres for Vesta and the Orion Nebula to make it possible to use the Fly-To feature with these objects (#2259)
 - Fixed a typo in the reset_loop_action.asset that prevented the asset from being able to be included
 - Fixed spelling mistakes in the Andromeda constellation image (#2129)
 - Fixed spelling mistake in Voyager focus action
 - Fixed missing GuiPath for Jupiter approach in Voyager profile
 - Update the descriptions for the Open Star Cluster Digital Universe asset

## Bug Fixes
 - Fix issue where parts of a globe would disappear when the settings of a heightlayer change (#2096)
 - Fix an issue where it was not possible to drag the SkyBrowser window in fisheye rendering mode (#2093)
 - Fixed an issue where executing a SessionRecording containing a wildcard character `*` in the property name fails to load (#2121)
 - Provide a better error message when failing to load a dataset for GlobeBrowsing layer
 - Fixed an issue where ScreenSpace images would be too dark by adding a gamma correction slider
 - Various compilation and UI fixes for Linux (#1479, #2111, #2123, #2163)
 - Fixed an issue where the conversion of a preexisting profile from version 1.0 to 1.1 would not rename the keypad numbers correctly, causing the new profile to fail to load (#2138)
 - Fix issue where the first row in the ScriptsDialog of the Profile Editor would be automatically selected (#2282)
 - Fixed an issue where the navigation state was not loaded correctly from a profile (#2143)
 - Fixed an issue where exporting the camera position to a Navigation State would lose precision
 - Provide a better error message when trying to edit a profile that does not exist (#2224)
 - Fixed an issue where special characters would not show in the keybinding panel correctly
 - Fixed issue that prevented the full range of values for the field-of-view slider in the SGCT configuration editor from being used(#2148)
 - Place some stricter limitations on the field-of-view settings in the SGCT Configuration editor (#2156)
 - Fixed an issue that what cause a SkyBrowser display copy from being removed properly (#2200)
 - Fixed an issue that would occur when the camera's focus node was removed (#2196)
 - Correctly use the default position of display copies of the SkyBrowser
 - Fixed an issue where the time component in the WebUI would flicker as time is progressing
 - Fix an error where the interpolation parameter for a camera path was out of range causing the Fly-To to fail occasionally (#2211)
 - Fixed issue where an asset in the Profile Editor would be selected if there wasa folder with the same name as the asset (#2154)
 - Fixed an issue that would prevent multiple files from being synced in a UrlSynchronization
 - Updated SGCT configuration files that where using a legacy user position


## Breaking Changes
 - The height offset of a GlobeBrowsing height layer was calculated incorrectly before, causing a flip in the sign.  Before, an offset of 1000 would cause the terrain to be _lowered_ by 1000m, not _raised_ by 1000m as expected.  With this version, this bug is fixed, but it might require some adjustments in existing profiles. **Fix**: Invert the sign of all `*.Settings.Offset`s in scripts that apply to Height Maps
 - The organization of the NASA TREKs asset files has changed as the old method caused many users to get "too long path" errors on Windows.  **Fix**: Any user-created profile that uses the NASA Treks files needs to be manually updated.


# Beta-11 [0.18.0]
- Version: 0.18.0
- Date: 2022-05-06
- Finished: [5877112103cdcb894695c214c21c15d2625fbe0b](https://github.com/OpenSpace/OpenSpace/commit/5877112103cdcb894695c214c21c15d2625fbe0b)
- See [Release Notes](http://wiki.openspaceproject.com/docs/users/release-notes/v0180.html) for user-focused highlights.

## Features
### SkyBrowser
This feature brings high-resolution astronomical images from the [AAS Worldwide Telescope](https://worldwidetelescope.org) into OpenSpace. The location of a selected image is shown in the 3D view inside of OpenSpace. 

### Camera paths (Fly-To)
This feature adds the ability to automatically fly the camera between different objects and between different navigation states. Currently, this feature only works when the time in OpenSpace is paused. A "Fly-to" or "Zoom-to" path will automatically pause the time and unpause it (if it was unpaused before) after completing the flight. Additionally, this feature enables the use of "Idle behaviors" that can either be triggered manually or by completing a Fly-to or Zoom-to flight that will make the camera do something interesting until the user interacts with the system again.
  - Adding procedurally generated camera paths (#1667)
  - Remove `OrbitalNavigator.LinearFlight` and instead add "Zoom to" helper functions (#1837)
  - Adding the ability to trigger an idle behavior for the camera after finishing a Fly-to or Zoom-to flight path (#1898)
    - Add an OrbitAroundUp IdleBehavior that rotates around the y-axis of the node instead of the z-axis
  - Automatically pause simulation time when starting a Fly-to or Zoom-to flight (#1832)

### Actions
Introducing "Actions" as first-class elements in OpenSpace to make repeatable changes. In prior versions it was possible to bin scripts to keybinds and use a "key-less keybind" to configure repeatable effects. The "Action" concept replaces this by encapsulating the changes in an Action and then provide the ability to bind a key to trigger an action instead. This also enables the reuse of "Actions" in other parts of the software. Older profiles that were made with previous version will be converted automatically on load with an Action identifier generated automatically.
  - Added Actions concept (#1708)

### Event System
Added a system that causes a specific list of events to be triggered automatically depending on the state in OpenSpace. This, for example, enables features to automatically fade an object's trial when flying closer to an object, but there are many more events that are defined in the system
 - Add implementation of the EventEngine to handle global event chains (#1741)

### User interface improvements
Various user interface improvements in the launcher and the in-game interface

#### Launcher
  - Add a new panel in the launcher used to create new SGCT configuration files.
  - Add a new panel to query the JPL horizons interface and being able to generate Horizons files based on that
  - Add ability in different Launcher panels to select profile properties from the ScriptLog of a previous OpenSpace run (#1780)
  - Explicitly sort file lists before showing them to the user in the Launcher and the Session recording which were presented non-alphabetically on MacOS (#1943)
  - Add the ability to choose the script from the ScriptLog in the ActionDialog and the additional script dialog including filtering and reloading the ScriptLog file (#2019)
  - Add warning to keybinding editor for duplicate assignments (#1461)

#### In-game
  - Add a new UI panel that shows a representation of the keyboard and all actions that are bound to keys
  - Add links to a tutorial page in the hamburger menu in the bottom left
  - Add UI elements that enables dynamic reordering of planetary layers
  - Add action dialog used to browse and trigger the available actions that are defined in the current scene
  - Reload UI after adding screen space renderables or assets (#1703)
  - Add the ability to enable and disable the Exoplanets and Skybrowser components for individual profiles (#1945)

### Various Enhancements
  - Changed the default format of window configuration files from XML-based to JSON-based. The old XML format is deprecated and will be removed in the next major release (#1795)
  - Add an asset (and load it in the provided profiles) to dynamically address some scaling based on the Operating System's DPI scaling (#1880)
  - Add preliminary support for multiple simultaneous joysticks (#1787)
  - Automatically use 66% of the monitor size by default instead of 1280x720 (#1883)
  - Pass information about the operating system to the version reporter script (#1865)
  - Add a new environment variable OPENSPACE_GLOBEBROWSING that is queried for the extra download files for offline planetary surface images 
  - Update CEF version which improves the responsiveness of the user interface (#1114)
  - Add the ability to define and use custom properties using the `openspace.addCustomProperty` Lua function (#2064)
  - Backwards incompatible change to the Astrocasting protocol that reduces the amount of data that is transferred while connected to an Astrocasting session (#1985)
  - Improve support for the handling of SpaceMouse input devices and XBox controllers (#1989)
  - Add error message when trying to access Gaia module on Mac (#843)
  - Add two properties to control the font color of the Rotation, Zoom, and Roll toggles (#1726) [Thanks BlueVista] 
  - Added SpoutFlatProjection type [Thanks Marco @ Elumenati]
  - Clean up the remainders of the native GUI to harmonize its organization with the WebGUI (#2060)
  - Make the font size of the Lua console dependent on the DPI scaling for increased readability
  
## Content
### New Assets
  - Add most of the image sequences available from NOAA’s Science-on-a-Sphere (#1863)
  - Add new assets provided access to a large number of NASA TREKs Moon, Mars, and Mercury layers layers (#888)
  - Add a new profile and assets that show the solar activity in July 2012, a time in which a few coronal mass ejections were ejected into the solar system
  - Add new asset containing the Starlink satellites (#1818) 
  - Add new asset showing the active satellites (#1805)
  - Add model-based representations of the Mars moons Phobos and Deimos (#1963)
  - Add a model for the Eiffel tower with an accompanying action to place the model underneath the camera location to be used for scale references
  - Add a large number of new actions that are useful in their own right, but also serve as examples for implementing new user-defined actions (#2077)
  - Add trails for the planets barycenters which are disabled by default

### Fixes to existing assets 
  - Update the general planetary spice kernel to a new version that extending the range of planetary positions to covering 1550-2650 (#2061)
  - Removed the Orion nebula model from the default profile
  - Updates to JWST profile
    - Add a new new animated model (#1759)
    - Update for the timing information to match the actual launch date
    - Add new kernels that show the position of JWST from the launch all the way to the orbit around L2 (#2085)
    - Add more target images
    - Add a [custom webpage](http://ui.openspaceproject.com/jwst_scripts/index.html) used to control the orientation of JWST
    - Add the Hubble telescope trail
  - Update the kernels used in the OSIRIS-REx asset (#1651)
  - Update to all Horizons-based trails to use VECTORS type ephemeridis that do not suffer from the light-travel offset inherent in the Observer type (#1434)
  - Updated the kernels used for the Perseverance landing
  - Update the Earth Terrain WMS to the new ESRI server
  - Correctly specify the bounding sphere for the ISS
  - Add the option to apply a color map to the values of the Quasars dataset from the Digital Universe
  - Fix issue with stretched Themis maps on Mars (#1707)
  - Update the data used to show the Gaia trail (#1817)
  - Correctly specify the model size of the Apollo capsules (#1718)
  - Correctly add the Mercury DEM layers (#1799)
  - Update the Pioneer model to include textures
  - Fix the image type for GHRSST L4 MUR sea temperature layer on Earth
  - Update the color map for the Gaia Apogee and Galah datasets
  - Set the correct radii for Bianca moon
  - Set the correct radii for Mimas moon
  - Remove the padding images from New Horizons that mess up instrument timings in the dashboard info in the New Horizons profile
  - Correctly parent the Gaia trail and model to the Earth Center to match the Horizons file (#1573)
  - Fix mistake that caused the Gaia spacecraft to not point away from the Sun anymore
  - Fix issue where the identifier of the Camera Velocity dashboard was wrong
  - Move the launcher image synchronization from base into the base_blank asset
  - Move the trail-related actions from the base_blank into the base asset
  - Add an action and event to automatically switch the Sun and SunGlare when approaching the Sun (#1914)
  - Add bounding spheres to many more renderable types (#1957)
  - The “Period” of a RenderableTrailOrbit is no longer converted from days to seconds when loading an asset (#1860)
  - Renamed the prefix for the constellation art by James Hedberg from `ConstellationArt` to `ImageConstellation` to provide a better search result when searching for “Constellation”

### Content Creation
  - Deprecate the use of the `asset_helper` file in exchange for explicitly writing the initialize/deinitialize functions (#1868)
  - Change the behavior of TemporalTileProviders to provide both a Folder based and a Prototyped mode (#1800)
  - Adding an ImageSequenceTileProvider that loads a folder of images and makes them available through a user-selectable index (#1798)
  - Add a new (hidden from UI) "Fade" property to enable the smooth fading of objects without messing with user's opacity (#1970)
  - Add the ability to ingest VECTORS type ephemeridis from Horizons (#1434)
  - Add properties to SceneGraphNodes to determine two distance radii for camera-based events
  - Add a new rotation type `GlobeRotation` with examples (#1737)
  - Interpolation of tiles added to tileprovider, with additional new shaders to make this work (#1769)
  - Add moon_minor tag for all minor moons
  - Implement new Spout input methods to tile providers and new Renderables (#1901) [Thanks Marco @ Elumenati]
  - Make the Sun asset export the Sun as a light source (#1870)
  - Replaced "UseAdditiveBlending" with "RenderBinMode" in some Renderables (#1842)
  - No longer require the filenames from a synced resource to start with a /
  - Add support for RenderableModel to take custom shader code with example (#1723)
  - Remove Fallback layer concept (#1819)
  - Remove the old virtual property code
  - Add new model format compatible with TurboSquid requirements (#1706)
  - Add support for DMS format support in the DashboardItemGlobeLocation (#1632)
  - Renamed “RenderOption” to “RenderMode” in RenderableGaiaStars (#2078)
  - Add a Lua-controllable State machine that can contain nodes and edges where transitions can be defined that execute Lua scripts (#1705)
  - Make the UTC function return the date in ISO 8601 format as advertised. Add SPICE function to get the old format (#1776)
  - Add ability to print all types of information in the printInfo/... functions and add the ability to pass any number of arguments to the function (#1635)
  - Add the ability to target the next interesting focus node as provided by the profile (#1717)
  - Add a Lua function to be able to read files from disk (closes #1636)
  - Add Lua script to manually sync or unsync resources (#1713)
  - Add Lua functions to get the bounding and interaction sphere values for a SGN
  - Add Lua function to get current application time

## Bug Fixes
  - Fix issue that would prevent Windows 11 from being detected correctly
  - Correctly specify tags and fix usage of "refreshRate" and "vsync" parameters (#1890)
  - Fix globe transformations not updating from height map if simulation time paused (#1766)
  - Prevent the loss of precision in the Launcher camera UI dialog (#1642)
  - Prevent a crash when a profile does not provide any Time or Camera information (#1981)
  - Prevent crash in DashboardItemInstruments when using dates before 2000 (#1878)
  - Add the current working directory correctly when registering the application's binary path
  - Fix issue that prevented AMD cards from being detected correctly (#1907)
  - Correctly destroy RenderableGalaxy shader when deinitializing (#1601)
  - Prevent some crashes from occurring trying to query non-existing scene graph nodes (#1831)
  - Fix issue where the search bar would not show all entries in the Scene list (#1775)
  - Fix a crash when unloading GlobeBrowsing layers
  - Fix issue that prevents the drag-dropping of an image that has extra dots in the name (#1793)
  - Fix issue loading a colormap for the Gaia stars
  - Fix for a crash that happened occasionally when adding exoplanet systems (#1781)
  - Fix RenderablePlaneImageOnline not updating size on property change
  - Prevent the use of modifier keys as actual key bindings (#1744)
  - Prevent saving keybinds without a key as that leads to a crash (#1758)
  - Removed hard-coded path expectations to allow drag & drop playback (#1754)
  - Correctly display user assets in the asset selection GUI (closes #1739)
  - Avoid crash in AstroCasting when there is no connection
  - Fix GlobeRotation/Translation not updating if simulation time is paused
  - Add fix to raw tile reader size calculation that prevented the full resolution of a GeoTiff to be used (#1716)
  - Fixed timing issue when interpolating property values while playing back a session recording while writing out frames (#1690)
  - Don't disable the CEF UI when turning off Master rendering (#1699)
  - Reset the anchor/aim node when removing a scene graph node to prevent a crash because of the node missing (#1402)
  - Prevent resetting of empty tile providers which would cause a crash (#1383)
  - Increase the sensitivity in the DebugAxis to prevent loss of color in debug axis (#1560)
  - Prevent the failure of font loading from keeping file handles open and breaking everything else (#1627)
  - Explicitly check for NaN in camera setting which would sometimes lead to the camera borking out (#1686)
  - Don't accidentally delete someone else’s VBO and VAO in Atmosphere Deferred Caster (#1694)
  - Filter out non-image files from the launcher collection (#1693)
  - Add support for speck keywords that are mixed case (#1689)
  - Make the speck loader ignore tabs as well as spaces (#1688)
  - Provide error messages when loading a speck file that contains entries that are not numbers (#1903)
  - Fix for rendering atmospheres on Intel chips
  - Fix an issue that lead to misclassification of OpenGL versions
  - Fix mix-up with the enabled cube faces in the spout configuration
  - Fix issue that could lead to an unresponsive application when encountering FreeType errors
  - Improved numerical precision on scale value in sessionRecording files in ascii format (#1732)
  - Prevent the automatic detection of texture sizes that would prevent a, for example, 128x1 image to be used as a 2D texture
  - Support negative altitudes in GlobeTranslation
  - Fix for an issue that would lead to an infinite loop when loading an invalid Horizons file in a HorizonsTranslation (#1849)
  - Fix for a rendering issue where labels on planets would be rendered without depth testing (#1915)
  - Fix for rendering "DoubleProperty"s in ImGui that led to a crash when looking at the property list
  - Fix that prevented the playback of an ASCII session playback file with a script recording that contains a newline character (#1974)
  - Fix issue where playing back a session recording containing a multi-line script would fail loading (#1905)
  - Fix issue that could occur when there is an erroneous TUIO server sending input that are interpreted as touch inputs
  - Fix issue that would prevent the loading of map tiles from the Utah WMS server
  - Prevent a crash when using a colormap in the RendrableBillboardsCloud without entries or if the provided color map did not exist (#2082)
  - Fix an issue where the loading of NaN values from a speck file failed to work and would stop the file loading (#2054)
  - Fix an issue where a FixedRotation depending on the position of other nodes would not update correctly when the time is paused (#1751, #2069)
  - Fix a bug that would load the wrong profile when selecting a built-in profile with the same name as a user profile (#2074)
  - Fix issue where the colormap values for a custom coloring option in the RenderableStars were not loaded correctly (#2080)
  - Fixed an issue where the focus node would not be correctly reset after a session recording finishes (#2070)


## Breaking Changes
 - Renamed `RenderEngine.ShowOverlayOnSlaves` to `RenderEngine.ShowOverlayOnClients`
- Change how moveLayer works slightly, so it is easier to use in a GUI implementation
- Remove non-functioning ABufferRenderer from RenderEngine
- moveLayer indexing changed;  "newPosition" is now considered to be the item's new position (index) in the list
- Keybindings -> Actions transition; users need to first define actions and then bind to keybindings rather than just defining keybindings
  - Loading .scene files is no longer supported and files need to be converted to .profile files
  - `tileProvider` renamed to `TileProvider` and `adjustment` renamed to `Adjustment` in Globes
  - Linear flight removed and replaced with camera paths
  - Lua function renaming/changes
    - `getKeybinding` -> `keyBindings`
    - `getSpiceBodies` -> `spiceBodies`
    - `getSpkCoverage` -> removed
    - `getCkCoverage` -> removed
  - Renamed “RenderOption” property to “RenderMode” in the RenderableGaiaStars (#2078)
  - Renamed “openspace.walkDirectoryFolder” to “openspace.walkDirectoryFolders”
  - Removed non-functioning “openspace.saveLastChangeToProfile” function


# Beta-10 (Patch-2) [0.17.2]
 - Version: 0.17.2
 - Date: 2021-08-27
 - Finished: [3a81662dd2e76bfb1c88c08449e1119a66965d2b](https://github.com/OpenSpace/OpenSpace/commit/3a81662dd2e76bfb1c88c08449e1119a66965d2b)

### Features
 - Added Enabled/Disabled color customization to RenderEngine (partially address #1697)

### Content
 - **Updated Earth terrain server to new ESRI server**
- Corrected the scale of Apollo capsule model (#1718)
 - Fixed image type for GHRSST L4 MUR sea temperature

# Beta-10 (Patch-1) [0.17.1]
 - Version: 0.17.1
 - Date: 2021-08-09
 - Finished: [c5b71d13a5b9d893448f7ddddbc7ecb6df4e1044](https://github.com/OpenSpace/OpenSpace/commit/c5b71d13a5b9d893448f7ddddbc7ecb6df4e1044)

### Features
 - The DashboardItemGlobeLocation now prints the camera location in more standard GPS coordinates in Degrees, Minutes, and Seconds (DMS) (#1632)
 - Automatically reload the WebUI after a drag & drop event (#1703)
 - An info message is printed when an asset is added via drag & drop
 - Added option to the OpenGL Debug layer to print a stacktrace (#1700)
 - Removed the option of changing the rendering to the (already non-functioning) A-Buffer

### Content
 - Corrected the parent of the Gaia spacecraft trail (#1573)
 - Fixed model assets with incorrect (outdated) syntax (#1692)
   - Pioneer models
   - Apollo boulders

### Content Creation
 - Profile Editor keybindings panel can have multiple binds of same key (#1461)
 - Added the ability to read a file through Lua (`openspace.readFile`)  (#1636)

### Bugfixes
 - Fixed an issue where planet atmospheres are not rendered on Intel GPUs
 - Fixed a crash when resetting tile provides on a RenderableGlobe without layers (#1383)
 - Fixed an issue where the resetting of font sizes would cause file handles to overflow
 - Fixed an issue that would double frames in Session Recording when in 'Output Frames' playback mode (#1669)
 - Fixed an issue where the scripting print functions do not handle all return values correctly and reliably (#1635)
 - Fixed an issue where the ConstantRotation transform doesn't respect non-incremental time changes (#1681)
 - Fixed a crash when removing the scene graph node that the camera is currently focused on (#1402)
 - Fixed an issue that prevented loading a prespecified SGCT configuration file through the launcher (#1624)
 - Prevent setting camera position to NaN under weird circumstances (#1686)
 - Fixed an issue where disabling the `Master rendering` option also disables the UI and client renderings (#1699)
 - Fixed an issue where speck file containing tabs were not loaded correctly (#1688)
 - Fixed an issue where speck files with different capitalization of keywords were not loaded correctly (#1689)
 - Fixed an issue with the debug axis causing a color loss in scaling (#1560)
 - Fixed an issue with Launcher background showed gray instead of an image; Launcher image search now ignores non-png files (#1693)

# Beta-10 [0.17.0]
 - Version: 0.17.0
 - Date: 2021-07-16
 - Finished: [3025fbc200ffdd8cf80f95c5f251d0daf793fbdf](https://github.com/OpenSpace/OpenSpace/commit/3025fbc200ffdd8cf80f95c5f251d0daf793fbdf) 
 - See [Release Notes](http://wiki.openspaceproject.com/docs/users/release-notes/v0170.html) for user-focused highlights.

### Features
 - Added drag and drop support for images and assets (#1497)
 - Added central location for user profiles, assets, screenshots and config files. Making it easier to upgrade OpenSpace versions.
 - Added support for multitexturing of 3D models
 - Added support for 3D model animation
 - Added logarithmic sliders and color picker (#1564)
 - Added the ability to remap SPECK variables to usage values for star data (#1598)
 - Multiple new Session Recording features
    - Fixed-frame rate playback for HD rendering playback
    - Time rate at beginning of recording is preserved
    - For every property change made during a recording, a corresponding property command is added to the start of the file to preserve its initial conditions
    - A recorded file is parsed before playback starts, and is rejected if it contains assets that are not currently loaded
    - Pausing during playback is now supported
    - A reject list will prevent certain scripts from being recorded (which might interfere with playback or with editing playback files)
    - Now records to timeline in memory, saving to disk when recording has stopped
 - Added equirectangular_gui config for YouTube360 output
 - Added the ability to specify RenderEngine font sizes in the configuration file (closes #1653)
 - Added functions to convert a cartesian coordinate to a ra dec distance

### Content
 - Added habitable zone for exoplanet systems (#1436) and our Sun
 - Added 1 AU size comparison ring for exoplanet systems (closes #1413)
 - Updated ISS model
 - Updated DU Kepler planetary candidates data version
 - Updated the constellation art (closes #1553)
 - Added Titan atmosphere
 - Added new asset to show a target marker (closes #85)
 - Added ESRI MOLA_HRSC DEM and made default for Mars
 - Added Pluto Kepler trail and descriptions to Pluto trails
 - Changed default texture for newhorizions profile
 - Added jwst profile (#1611)
    - Added 3D model of the James Webb Space Telescope
    - Added trail of JWST orbiting L2
    - Added L2 position, marker, and line from earth
    - Added safe-viewing band for JWST
    - Added view frustrum for JWST
    - Added Hubble Deep Field image
    - Added other Lagrange points
  - Updated osirisrex profile (#1623) 
    - Updated files for OSIRIS-REx return
    - Changed osirisrex assets to bring mission events up to date
    - Added hi-res 75cm Bennu model from asteroidmission.org
  - Removed camera as light source for New Horizons model

### Content Creation
 - Specify of Atmosphere in assets no longer needs the `Atmosphere` parent table
 - Bring back fading of sphere with only fade out threshold specified
 - Added examples for all grid types
 - Added USGS WMS layers for Phobos and Deimos; moved them to planets.asset to be consistent with other solar system moons
 - Improved documentation for renderables
 - Added missing documentation for NonUniformStaticScale
 - Added examples for circle, ellipse, and elliptic disc
 - Enabled support for single double radius in SizeReferenceTileProvider (closes #1562)
 - Added ListProperties and SelectionProperty (#1558)
   - Added string list property tests and structure test files
   - Added IntListProperty, DoubleListProperty
 - Added GlobeTranslation Documentation to exported documentations (closes #1566)
 - Removed unused parameters and document the remaining properties of RenderableGlobe (closes #1470)
 - Enabled Screenspace renderable to have a multiplicative color 
 - Fixed missing documentation for time.interpolateTime 
 - Added fixed time for spice translations and rotations
 - Added simple animation example asset

### Bugfixes
 - Fixed Deep Sky Objects basic unit and increased maximum scale range (#1452)
 - Fixed reading of newhorizons files
 - Updated newhorizons.profile
   - Fixed error that the shadow of Charon is not toggled with Shift+T (closes #1463)
   - Fixed syntax error in A key (closes #1464)
 - Fixed for issue #1453 MODIS water mask update
 - Avoided adding too many delta time step keybindings (closes #1445)
 - Small grid renderable updates/fixes (#1473)
   - Fixed problems with blending when rendering transparent grids
   - Fixed issue with resizing box grid
   - Avoid problems with line width on Mac
 - Globebrowsing fade-in/out fix and assets updates (Issue #1209) (#1476)
   - Fixed fade out algorithm to use correct distance from globe center
   - Updated planet labels in asset files to match fixed fade-out algorithm
 - Fixed issue with the item velocity not showing up correctly and with varying lengths
 - Fixed a crash when reloading a browser instance twice in quick succession
 - Fixed for HiRISE Local Set DEM from ESRI
 - Fixed Pioneer model, added meta info
 - Fixes for issue #1409 (#1501)
   - Fixed renderablesmallbody selective rendering props to accept asset file settings
   - Mirror selective rendering behavior from smallbody to satellites
   - Added property coupling of values to satellite/asteroid render settings for size, start index, upperlimit
   - Improvements to documentation and handling values spec'd in asset file
   - Fix for satellites: selective rendering settings specified from assets
 - Prevent renderbin change for overlay renderables (#1519)
 - Fixed labels not facing the camera due to static rotation (closes #1542)
 - Prevent crash when reloading renderable that only has labels and no data
 - Updated Apollo models for new model code
 - Ignore joystick input in deadzone, fixes #678
 - Prevent setting zero line width from UI
 - Fixed an issue that prevented the spheres from being rendered
 - Increased scale height for Venus atmosphere (closes #922)
 - Simplified Property code (#1575)
   - Solved a bug in SelectionProperty that occurred when re-setting options
 - Fixed that allows all days of month except monthly increment still at 1-28 for TemporalTileProvider
 - Renamed PerSceneCache to PerProfileCache and make it work again (closes #1577)
 - Only use the adaptive level-of-detail when actually rendering out frames in a session recording (closes #1292)
 - Actually make use of the model matrix in the atmosphere radius calculation for determining whether it should be culled (closes #1465)
 - Fixed issue when trying to print non-ASCII character
 - Fixed interpolation problem with playback of session recording in HD (#1373)
 - Fixed session recording needs initial simulation time rate to be saved in file (#1506)
 - Fix for Voyager 2 trail (#1582)
 - Fixed side by side rendering (PR #1613) 
 - Fixed an issue with syncing Gaia profile
 - Fixed misaligned surface textures for Callisto, Europa, Jupiter, Titan, and Saturn
 - Mostly eliminated an issue where planets disappear when changing focus (#1455)
 - Reduced risk of font rendering errors from user interaction (#1206 hot fix) (#1616)
 - Fixed Voyager spelling mistake
 - Updated documentation for bindkey
 - Fixed broken referencing links in documentation
 - Fixed issue when RenderableBillboardsCloud had data without colors
 - Read Horizons file with double precision
 - Fixed some small issues with trail identifiers
 - Comment out FOV for REXIS as it has an unsupported shape (closes #1650)
 - Prevent NaN values in StaticTranslation by limiting min and max size 
 - Added exponent to GlobeTranslation altitude slider
 - Correctly pass in the irradianceFactor into the inscatter radiance for atmosphere (closes #1660)
 - Avoid non-supported ranges for exponential slider (#1672) 
 - Fixed issue with interrupted fisheye rendering between cube maps (closes #1275)
 - Fixes to fullscreen1080 and spoutOutput config files
 - Adapt addFocusNodes for GlobeTranslation

### Enhancements
 - Added module property for exoplanet habitable zone opacity
 - Speed up for `setPropertyValue` function
 - Improved Saturn rings
 - Make use of new verifiers (Color and File) (#1510)
 - Added a colored glare to exoplanet stars (#1511)
 - Removed hardcoded path to B-V colormap (#1531)
 - Added property to determine whether the date should be added to the screenshot folder (#1535)
 - Added dialog for choosing scripts from the script log (#1539)
 - Added a scriptlog dialog field to the additional scripts box
 - Enable setting of opacity for RenderableGlobe (closes #1449)
 - Feature/galaxy (#1576)
   - Remove translation from renderablegalaxy
   - Apply additive blending when compositing downsampled volume;  Use star distance as alpha for transparency (closes #1208)
 - Added the ability to specify a specific time for a TemporalTileProvider (closes #1171)
 - Feature/interactionsphere (#1561)
   - Added ability to render the bounding sphere as a debug option
   - Separate boundingsphere and interactionspheres
 - Feature/speck loader (#1585) unified code for loading .speck files
 - Enabled joystick interaction by default
 - Added the ability to RenderableFOV to always draw the field of view frustum
 - Increased the number of objects and windows that are extracted from SPK and CK files
 - Updated SPICE library to N0066, build spice as static library to improve performance slightly
 - Added base texture or color to ModelProjection
 - Centered shutdown warning and a dimming of the rendering
 - Feature/render at distance (#1665) adding option to disable distance check for globes
 - Added the ability to optionally ignore the scale value read from session recordings
 - Added new images to OpenSpace Launcher

## Breaking Changes
 - Remove the ability to render AABB for globes as it caused a circular dependency between GlobeBrowsing and Debugging
 - Renamed `AtmosphereRadius` -> `AtmosphereHeight` and `GroundRadianceEmittion` -> `GroundRadianceEmission`
 - Changes specification of Shadowgroups in Atmosphere to be list-based
 - Rename `GridColor` to `Color` for better consistency among renderables
 - Updated pioneer identifiers to allow spice and horizions to coexist
 - Move default_dashboard asset from util folder to new dashboard folder that also includes the individual dashboard items
 - Include strict lua file, throw error in configuration loading when overriding with unused variable
 - Feature/numeric slider updates (#1609) Renderables with rename properties: `RenderableLabels , GlobeLabelsComponent, RenderableBillboardsCloud, RenderableDUMeshes, RenderableRadialGrid` ) see [https://github.com/OpenSpace/OpenSpace/commit/169593774976b7389f1d3c921e2074e8a701d000](https://github.com/OpenSpace/OpenSpace/commit/169593774976b7389f1d3c921e2074e8a701d000) for details.
 - Switch use of Spice id SUN to SSB where SSB is parent
 - Place planets in their centers and not barycenters
 - Separate the different joystick configurations into their own assets
 - Update faulty docs and function name for getGeoPosition (#1662) (#1677)

# Beta-9 [0.16.1]
 - Version: 0.16.1
 - Date: 2021-05-07
 - Finished: [452d4e9626c58629709c7ed061fedc7141964727](https://github.com/OpenSpace/OpenSpace/commit/452d4e9626c58629709c7ed061fedc7141964727)
 - See [Release Notes](http://wiki.openspaceproject.com/docs/users/release-notes/v0161.html) for user-focused highlights.

### Features
 - Added Drag and Drop support for images and assets (#1497)

### Content
 - Added USGS WMS layers for Phobos and Deimos

### Content Creation
 - Added missing documentation for RenderableOrbitDisc
 - Added the ability to use single radius for SizeReferenceTileProvider (#1562)
 - Fixed an issue with the example asset for spheres

### Bugfixes
 - Fixed the keybinding-related loading error in the newhorizons and mars profiles
 - Fixed an issue that would add too many delta time step keybindings (#1445)
 - Fixed a crash that could occur when trying to reload the in-game browser twice in quick succession
 - Fixed an issue where the joystick input was completely ignored in the deadzone and cause erratic behavior (#678)
 - Fixed an issue where the milkyway sphere would not fade out correctly
 - Fixed an issue where the labels of the grids would not be aligned correctly towards the camera (#1542)
 - Fixed problems that prevented the 'gui_projector.xml' and 'spherical_mirror.xml' from working
 - Fixed an issue that prevented the ESRI Local Set DEM from showing up
 - Prevent the change of renderbins for overlay renderables, causing incorrect behavior for transparency (#1519)
 - Fixed issues with the Pioneer model and updated identifiers to allow SPICE and Horizons versions to coexist (thanks Dan Tell)
 - Fixed an issue where the slide deck functionality was no longer working (#1441)
 - Fixed an issue where the Deep Sky Objects were scaled incorrectly by a factor of 1e6 (#1452)
 - Fixed a bug that prevented the correct showing of color properties
 - Fixed an accidental commit in the globebrowsing customization asset
 - Fixed a bug that caused the item velocity dashboard item numbers not to show correctly
 - Prevent a crash when reloading a renderable that only has a label, but not data
 - Prevent a crash when trying to query the renderable of scenegraph nodes that don't exist
 - Don't produce OpenGL performance warnings on Intel chips, leading to noisy logs

# Beta-8 [0.16.0]
 - Version: 0.16.0
 - Date: 2020-12-10
 - Finished: [c13b211add7b1bc4336de34ee6cb4f6064420242](https://github.com/OpenSpace/OpenSpace/commit/c13b211add7b1bc4336de34ee6cb4f6064420242)
 
## Changelog
See [Release notes](http://wiki.openspaceproject.com/docs/users/release-notes/v0160.html) for user-focused highlights.

### Features
- Add new 'Profiles' feature that replaces the `*.scene` files with a more descriptive format that enables editing with a graphical user interface
  - Added a more rigorous way to specify the delta times in a profile (#1285)
  - Added new user interface for editing Profiles and selecting which profile and configuration to use at startup
- User interface improvements
  - Added new user interface for adding Exoplanets (#1304)
  - Added new user interface panel to remote control an OpenSpace instance. This panel is only shown when connecting to a running OpenSpace instance via an external browser by going to localhost:4680
  - Added a button to the user interface to step between delta times from the Date/Time panel
  - Added information icons to the user interface that show the information stored in the Meta field of the assets
- Large performance improvements across the software (loading time and rendering) (#1270, #1271)
  - Horizon translation files are now cached between starts of OpenSpace, improving the startup time (#1185)
- Fixed the code so that it can be compiled and run on MacOS again
- Added the ability to step between delta time steps using the arrow keys (#1174)
- Automatically bind the negative delta time key by using the "ALT" key.  For example if "Shift+5" is mapped to a delta time of `30`, "Alt+Shift+5" will automatically be bound to `-30`.
- Added a new field to assets and profiles that contains meta information about the asset, such as license information, author information, and additional description
- Added the ability to change the focus node without resetting the cameras velocity (#1276)
- Session recording improvements
  - Added the ability to have # deliminated comment lines in the session recording file for use in scripting
  - Introduced a breaking change by changing the binary folder of the session recording from using a 64bit script length to a 32bit script length. All session recordings will automatically be converted without the need for user action. The converted session recording file will be stored in the `recordings` folder
  - Added `osrec` and `osrectxt` extension to session recordings
  - Provided a Task that converts text-based session recordings to binary and vice versa
- Added a property in the RenderEngine to be able to soft-cap the framerate without restarting OpenSpace
- Added an alternative location for the sync folder to the openspace.cfg file that tries to find a `OPENSPACE_SYNC` environment variable. If such a variable is set, it is used for the location of the sync folder, making it easier to reuse sync folders between OpenSpace installations
- Added a new Native-GUI (ImGui) component to load planetary labels from NASA GIBS
- Added a property that disables joystick input to prevent erratic input on startup (#1370)
- Added the ability to skip a range of screenshots when rendering out a long sequence
- Added the ability to vertically offset the screenlog so that it is not covered by the user interface
- Added the ability to change the screenshot folder at runtime (#1172)
- Enabled OpenGL debug context by default for now to prevent large frame stuttering until a more permanent solution is implemented
- Added a notification when OpenSpace is compiled with Tracy support (#1189)
- Updated the CFITSIO library
- Updated the GLFW library

### Content
- Added a method for dynamically adding all known Exoplanets to the scene (#919, #1303)
- Split up all provided globebrowsing layers into individual assets such that they can be loaded/ignored by a Profile UI (#1259)
- Added a polygonal model of the Orion Nebula
- Added the C/2019 Y4 comet to the astroids scene (#1201)
- Added trimmed-down version of the Voyager/Pioneer trails that omit the models
- Updated James Hedberg's constellation images (#1263)
- Added shadowing of Jupiter's main moons onto Jupiter (#1426)
- Removed the multiple lookback perspective viewpoint CMB representations out of the `cmb.asset` and into their own asset file which no longer gets included by default in the `base.asset`
- Updated the keys for the slide deck example from Left/Right/Up to KP_4/KP_6/KP_0 to not collide with the new delta time keys (#1320)
- Added missing tags to the Pluto system (#1319)
- Removed the "L4 G1SST" Earth layer with the "GHRSST L4 MUR Sea Surface temperature" (#1204)
- Added an explicit `digitaluniverse.asset` file that is used in the `base.asset` instead of the previous `requireAll` function call (#1398)

### Content Creation
- Removed the `asset.request` in favor of only using `asset.require` (#1280)
- Unify the usage of the color + transparency/opacity for all renderables (#1196)
- Added a new radial grid in addition to the rectangular that already existed (#733)
- Added the ability to use linear interpolation in a color map for the RenderableBillboards
- Added a new function to procedurally create a grid without needing to create a SPECK file first (#733)
- Added the ability to render out the current recording time during a session recording
- Added a `BoundingSphere` parameter to SceneGraphNodes to manually specify a bounding sphere radius for objects that can't compute one automatically (#1238)
- Made the `LabelText` in `RenderableLabels` optional (#1237)
- Added the ability to toggle planets in the `customization/globebrowsing.asset` (#1392)

### Bugfixes
- Fixed issue where the normals of the ISS would look wrong in Fisheye rendering
- Corrected the orientation of the digital universe's radiosphere (#1223)
- Fixed issue where the trails would not show up properly when intersecting an atmosphere (#1217)
- Fixed issue where the eclipse shadow would not scale when the shadowing body is enlarged (#1160)
- Fixed issue that would prevent Earth from rendering with multiple Night-side layers (#1323)
- Fixed an issue that would cause flickering of planetary atmospheres when the milky way sphere was disabled (#1360)
- Fixed an issue where the camera would become invalid when selecting a linear flight distance of 0 (#1329)
- Fixed error with capitalization of maps on Mercury that prevented them to be loaded on operating systems that care about capitalization (#1260, thanks John Riedel)
- Fixed the wrong printing of error messages when loading a completely fine astroid dataset
- Fixed an issue in curved-scree nrendering where the DigitalUniverse representations would change size when moving to the corner of a projector (#1354)
- Corrected the size of Phobos and Daimos
- Fixed an issue where the speed of the linear flight was not taking the framerate into account (#1369)
- Fixed flood of warnings when trying to enable accurate normals for planetary surfaces without a heightmap (#1421)
- Fixed the name of Kerberos' trail
- Fixed a crash when setting the point-spread function texture for stars to a file that didn't exist (#1222)
- Fixed a bug that caused the highest resolution map layer on planetary bodies to be ignored
- Fixed bug that prevented labels from appearing (#1278)
- Various fixes to make OpenSpace compile and run in Linux-based operating systems
- The ISS is not correctly cleaning up after itself (#1318)
- Fix issues with the SPOUT transmission of the rendered image
- Fixed issue that would lead to the wrong height being used in the LuaConsole (#1375)
- Fixed a warning that would appear when trying to switch to a non existing slide deck image with 0 interpolation time (#936)
- Fixed issue where the extension of screenshots would be missing in some cases
- Fixed UI bug where it would show -1sec/sec as "Realtime"
- Fixed issue where OpenSpace would warn about an empty folder when loading the `customization/globebrowsing.asset`
- Fixed issue where the 'swiftshader' folder in the bin folder would appear recursively

## Breaking Changes
1. The previous loading of `*.scene` files is no longer officially supported.  The suggested mitigation is to recreate the scene files using the new Profile editor or manually converting the `.scene` files into `.profile` files.  For logic that was previously performed in a scene file, we recommend either (a) adding a new `.asset` file with that logic as the last asset in the profile or (b) provide that logic in the _Additional Scripts_ section of the Profile.  Please note that the delta time keys are no longer bound manually in the file, but should be specified in their _Delta Times_ section of the Profile instead.  That will cause them to be bound to the expected number keys also also bind the negative version to the ALT key.  For example if "Shift+5" is mapped to a delta time of `30`, "Alt+Shift+5" will automatically be bound to `-30`.
1. The handling of colors in the asset files and scripts has significantly changed.  Where previously some assets would use an (RGBA) 4-vector to combine the opacity and the color, this is now separated.  All colors are only specified using an (RGB) tuple and an *additional* `Opacity` value that specifies the opacity of the object.  Additionally, all instances of `Transparency` were converted to `Opacity`. Additionally, the `ScreenSpaceRenderable` classes were using "alpha", which has also been renamed to "opacity"
1. The `asset.request` function was removed in favor of `asset.require`.  All use cases of `asset.request` can be achieved by calling `asset.require` instead
1. Joystick input has been disabled by default and needs to be reenabled through a property in the NavigationHandler, if so desired.  The unexpected input of non-calibrated joysticks was jarring for a number of users and we feel that the default behavior should be to ignore joystick inputs

## New Software
The team has been working hard on providing a tool to start OpenSpace in distributed environments where it might be cumbersome to start OpenSpace (or any other application) manually on each computer.  See the _C-Troll_ application (https://github.com/c-toolbox/c-troll) for more information.

# Beta-7 [0.15.2]
 - Version: 0.15.2
 - Date: 2020-06-22
 - Finished: [076a96e651a59cc9f330ef94c09259db2dbd41de](https://github.com/OpenSpace/OpenSpace/commit/076a96e651a59cc9f330ef94c09259db2dbd41de)
 
## Changelog
### Features
 - Added new meta information to the assets that is automatically collected into the documentation/index.html to provide direct information about the license state of the current scene
 - Added a new version of SGCT that should improve performance and future extensibility
   - Added support for cylindrical and equirectangular output methods
 - Added a feature for touch interface to enable a continous pinch gesture to continue to zoom in without the need to repeat the pinch gesture 
 - Added the ability to change the line width of wire-type meshes (#1153)
 - Added the ability to invert mouse buttons (#697)
 - Added the ability for a vertical offset for a screen log
 - Added a property for line width to the constellation bounds (#1214)

### Content
 - Added a model and the trajectory of the Mars 2020 Perseverance rover
 - Added a new, fully-textured model of the International Space Station
 - Added new asteroids datasets from JPL Horizons (#1123) -- see [asteroids content page](http://wiki.openspaceproject.com/docs/users/content/asteroids#asteroid-content-categories) for categories included
 - Replaced the L4 G1SST sea surface temperature with the GHRSST L4 MUR as it is a wider coverage (#1204)
 - Added new constellation images (thanks to James Hedberg)
 - Added the C/2019 Y4 (ATLAS) comet (thanks to Dan Tell)
 - Added time range to Voyager rotations to make that scene more useful
 - Fixed spelling errors with Uranus label and the CTX surface layer
 
### Content Creation
 - Added the ability to load images for planes lazily
 - Added suport for non-uniform static scaling of objects (#1151)
 - Added a new renderable that shows customizable distance labels between scene graph nodes

### API
 - The `openspace.sessionRecording.enableTakeScreenShotDuringPlayback` function now has a default framerate of 60 (#1134)
 - Added support for the Tracy profiling library to debug performance issues
 - Added more meaningful error messages to the `openspace.globebrowsing.addBlendingLayersFromDirectory` if the parameters are missing (#1101)

### Bugfixes
 - Fixed issue with time quantization for temporal globe browsing layers that could cause the displayed image to be off by 1 day (#1092)
 - Added fixes to enforce a 0-360 angle range on incoming data from JPL Horizons
 - Various fixes to make the touch interface more reliable on Windows
 - Compilation fixes for Clang on Linux
 - Removed the highlight created by the operating system when using touch on Windows
 - Better handling of touch interaction for the native ImGUI user interface
 - Removed warnings that occurred when disabling all night layers on Earth (#1136)
 - Added fix for leap year in the calculation of the satellite orbits
 - Fixed a bug where the static rotation was not updated when changing the Euler rotation angles
 - Fixed an issue with rendering the renderable grid
 - Fixed issue that made it difficult to view the cosmic microwave background radiation image from Earth
 - Improved the performance of the Borisov trajectory rendering
 - Fixed the positioning of the Apollo 8 trail around the moon
 - Fixed an error with the orientation of the Digital Universe deep-sky objects
 - Fixed a rendering issue that made the grids flicker

# Beta-6 [0.15.1]
 - Version: 0.15.1
 - Date: 2020-02-17
 - Finished: [9c34a55e50d7039c4408d2d0f8f9b0e73fc93bdc](https://github.com/OpenSpace/OpenSpace/commit/9c34a55e50d7039c4408d2d0f8f9b0e73fc93bdc)

## Changelog
### Features
 - Added a new rendering feature that uses the rings of saturn to create shadows onto Saturn and vice versa
 - Added a new rendering method for anti-aliased trails that improve their visual look at feel
 - Improve the handling of touch input on Windows systems that no longer requires started a separate TUIO server.  This also improves the handling of the touch input.
 - Improved the automatic generation of unique names for screen space renderables
 - Added a bookmarks file that will automatically create scene graph nodes to be able to focus on interesting locations
 - Added a new property that makes it possible to disable all mouse input
 
### API
 - Fixed retrieval of navigation state from the `openspace.navigation.getNavigationState` function and make this function usable again
 - Added a script that enables to directly add a layder from GIBS `openspace.globebrowsing.addGibsLayer`
 - Updated GLM version to 0.9.9.6
 - Replaced Google Test framework with Catch2
 - Added basic functionality for Tracy profiler
 - Added CMake options to build targeting an AVX, AVX2, or AVX512 processor architecture

### Content
 - Added ISS asset to the default scene
 - Added asset for C2019 Q4 "Borisov" interstellar object
 - Added over 2,000 identified Potentially Hazardous Asteroids (PHAs) from JPL Horizons
 - Added a WMS server for the Venus Magellan dataset
 - Added alpha channel to Kaguya layer
 - Added an atmosphere to Venus
 - Added the ability to display procedurally generated text labels and added labels for planetary bodies in the solar system.  The default binding to toggle their visibility is `L`
 - Added the ability to fade satellite trails
 - Added a feature to render stars with a fixed color to make interoperability with Glue easier 
 - Fixes spelling of layer name for Sea Ice concentration
 - Fixed the milky way by using a static translation to offset it, rather than doing it in the shader code
 - Added missingSun marker in the Osiris-REx scene

### Content Creation
 - Added a new scene graph node type that renders a line between two scene graph nodes
 - Added a new scene graph node type that shows the distance between two scene graph nodes

### Bugfixes
 - Fixed a rendering error in which the stars would be cut between viewports when rendering OpenSpace using a fisheye configuration
 - Fixed a bug where the application would crash when changing the segments property
 - Fixed a bug that prevents the removal of globebrowsing layers
 - Fixed a bug that made the atmosphere disappear when night or water layers weren't active
 - Fixed a bug that would cause temporal tile layers to be out of sync by a day
 - No longer assume that the GuiName for a DashboardItem is provided
 - Fixed a bug with the Dawn scene
 - Fixed duplicate keybinds in the rosetta scene
 - Fixed issue with the Mercury magnetosphere 
 - Added a fix where it was not possible to use a group name in the `getProperty` Lua function
 - Fixed bug in which OpenSpace would crash when an asset includes itself
 - Fixed error when loading some Linux-generated speck files on Windows
 - Fixed an issue to make OpenSpace work on CentOS with an older curl version
 - Fix a bug where the debug mode would not work because the website URL was empty

### Optimizations
 - Tweaked the message pumping of CEF to improve the UI responsiveness on Windows
 - Improved the loading time of the galaxy dataset by caching the star points using a binary file format
 - Drastically improved the rendering speed of the milky way volume by adaptively downscaling the rendering resolution
 - Improved the rendering performance of the billboard clouds used for galaxy points

# Beta-5 [0.15.0]
 - Version: 0.15.0
 - Date: 2019-09-17
 - Finished: [c3b481f1e9b340cda49147ce8c7eb2f99fc98f53](https://github.com/OpenSpace/OpenSpace/commit/c3b481f1e9b340cda49147ce8c7eb2f99fc98f53)

## Changelog
### Features
 - Added a partially linearized rendering pipeline that enables support for High Dynamic Range objects. This feature also adds support for changing the exposure of the virtual camera, enable tweaking of saturation, hue, and brightness of the overall image
 - Added a new, preliminary, profile creator to easily select which assets are included and save these as `.scene` files
 - Added a preliminary feature to perform offline rendering, which has to be enabled through the Lua interface as of now. When calling
`openspace.sessionRecording.enableTakeScreenShotDuringPlayback(framerate)`, the next playback of a session recording will create a PNG file for each frame while playing back the session recording at the selected framerate
 - Added a new feature that enables the control of the camera through a WebSocket API.
 - Added a new rendering method that enables a more efficient rendering of satellite trails
 - Added the ability for the user to specify the location of the temporary folder, which now defaults to the OpenSpace/temp folder, rather than a global operating system specific folder that is used between multiple applications

### UI Improvements
 - Added a new user interface to add online screen space images
 - Added support for multiple endpoints in the WebGUI
 - Allow the user to abort the loading screen through the ESC key

### API
 - Replaced old setCameraState with new function setNavigationState that works more consistently when in orbit around a planet
 - Added support for arrays in LuaScript topics
 - Exposed the GlobeTranslation properties correctly

### Content
 - Added a volumetric representation of the milky way
 - Added asset for the Apollo 11 descent
 - Added asset for the Swift-Tuttle comet
 - Added asset files for the Tesla roadster and Oumuamua interstellar objects
 - Fixed issue where the wrong identifier was used for requested the model data for Vesta
 - Add option to show information about the current frame and synchronization status in a HUD rendering
 - Added documentation and verification for the creation of globe browsing layers to detect missing or wrong keys
 - Added a new default configuration that contains a Fisheye rendering window and a GUI window
 - Removed the F4 performance measurement keys from the `base.asset`.  The performance window is still available through the old UI (F1)

### Content Creation
 - Added a new TimelineTranslation that interpolates between different Translations based on the in-game time
 - Added a new TimelineRotation that interpolates between different Rotations based on the in-game time

### Bugfixes
 - Fixed a bug where a joystick/gamepad would become unresponsive when changing the sensitivity
 - Fixed issue where the DashboardItem displaying the location on a globe would display negative altitudes correctly
 - Improved issues with the usability of the touchbar on MacBooks
 - Fix issue with uint32-limited tilecache size in bytes restricting larger caches
 - Fixed problem with zoom restrictions at min/max zoom levels when using the touch interface
 - Added fix to prevent starting a session recording/playback if another is already in progress.
 - Fixed problem where the atmosphere stereo separation was not correctly computed
 - Added a check to prevent sync buffer overflows when sending enormous Lua scripts >4KiB
 - Fixed a scaling issue with the screen space images
 - Fixed crash when requesting a local screen space image whose file did not exist
 - Fixed an issue where the download size of files >2GiB was not displayed correctly
 - Fixed an issue that prevented the WebGUI from starting on MacOS
 - Fixed an issue where the camera would jump a small bit when refocussing close to a planetary surface
 - Fixed a crash that would occur when trying to read two-line element files whose file on disk would not exist
 - Fixed an issue that would prevent runtime removal of more than one asset file
 - Fixed an issue where the wireframe sphere would not be rendered correctly when an uneven number of vertices was selected
 - Fixed an issue with the commandline parsing that would cause the application to hang indefinitely
 - Fixed an issue where the normal in camera space was not set for local globe browsing patches
 - Fixed a problem where the ephemeris information of Pluto expired on 2019-03-01
 - Fixed a problem in which the PerformanceManager would crash when enabled by the user

### Optimizations
 - Replaced Multisampling Antialiasing (MSAA) for a faster Fast Approximate Antialiasing (FXAA) which improves performance and reduced the graphics memory footprint of the application
 - Drastically improved the performance and timing consistency of the Globebrowsing image loading
 - Used the more optimal `setPropertyValueSingle` instead of `setPropertyValue` Lua function in the `propertyHelper.invert` functions, which no longer causes unnecessary RegExp to be compiled
 
 
# Beta-4 (Patch 1) [0.14.1]
 - Version: 0.14.1
 - Date: 2019-06-04
 - Finished: [0a68b06823a0f4809150db5f649ac923560afc52](https://github.com/OpenSpace/OpenSpace/commit/0a68b06823a0f4809150db5f649ac923560afc52)

## Changelog
### Features
 - Turn fade-in value into a property and move away from dedicated fadeIn, fadeOut methods
 - Consolidated all documentation files into a single file

### Content
 - Add multiple CMB spheres to show multiverses
 - Added optional keybinds CTRL+I, CTRL+K, CTRL+O, and CTRL+L for situations where the keypad is not available
 - Added optional F12 keybind to create a screenshot if the PRINT_SCREEN button is not available
 - Added apollo 11 CSM orbits and mock LEM decent to the apollo_sites scene
 - Warn if keybinds are defined twice
 - Updated Apollo sites to new LEM model based on photogrammetry
 - Updated fixed Pioneer model
 - Updated the rosetta images to only download a single zip file that gets extracted

### Bugfixes
 - Add Shift+A keybind for New Horizons scene to set the Aim+Anchor method, restoring the A keybind to the previous usage
 - Read DefaultAccess parameter from the configuration file correctly
 - Fixed bug where the field-of-view settings on dome image generators would be broken
 - Fix a warning if interpolating a value using the setPropertyValueSingle Lua method
 - Various fixes in the New Horizons scene to make it operable
 - Various fixes for the Rosetta scene
 - Fixed keyboard shortcurts in OsirisRex scene
 - Rebound the Philae trail visibility from F to G so that it is not on the same key as the friction
 - Disable the Rosetta image plane on default
 - Automatically remove old delta time keybindings when new ones are set in order to prevent double-binding
 - Cleanup of Apollo scene shortcuts
 - Fixing Apollo 8 and flipbook shortcuts
 - Updated number of samples for configs to make gui work on MacOS
 - Fixed bug where the UI would not show up if the computer is not connected to the internet

# Beta-4 [0.14.0]
 - Version: 0.14.0
 - Date: 2019-05-20
 - Finished: [cdeaae5068444f09129c703c40c9733a7d47e7d1](https://github.com/OpenSpace/OpenSpace/commit/cdeaae5068444f09129c703c40c9733a7d47e7d1)

## Changelog
### Breaking changes
 - Renamed property owner identifier from renderable to Renderable.  For instance, the property `Scene.EarthTrail.renderable.Enabled` is now called `Scene.EarthTrail.Renderable.Enabled`, and likewise for all other items in the scene graph

### Features
 - Added session recording feature
> This feature enables the recording of camera movements and user interface interactions.  When playing a recording back later, all camera movements and state changes are occurring at the same times when they did during the initial recording.  The recording will start at the same in-game time and speed in which OpenSpace was when the recording was done.  Recordings can be shared between computers as long as they are played back on the same scene or otherwise strange behavior might occur.  There is a user interface to control the recording and there are Lua scripts available to start and stop the recording and playback `openspace.sessionRecording.startPlayback()`, `openspace.sessionRecording.stopPlayback()`, `openspace.sessionRecording.startRecording(<filename>)`, `openspace.sessionRecording.stopRecording()`, and others
 - Added support for the new web-based user interface based on Chromium Embedded Framework for MacOS
 - Added a new rendering methods for rendering star catalogues that improves the visual quality and provides future support for point-spread function based rendering methods.  Additionally, it adds the capability to inspect other data values that are available in SPECK files and map these to colors
 - Added an Anchor&Aim feature that enhances the previous Focus Node concept.  While it is still possible to focus the camera on a single object as before and have all camera movements occur relative to that object, it is not possible to aim at a second object which then stays fixed on the screen
 - Added the ability to change the field of view for the main rendering window at run-time.  Please be aware that this feature might have unintended consequences if multiple rendering windows with different field of views are shown on the same computer
 - Added an indicator showing the number of enabled layers for a globe and prevent the user from enabling too many layers simultaneously.  If too many layers are enabled, the last layer will be automatically disabled
 - Added the ability to rescale Web UI during run-time
 - Added the ability to position screen space objects in 3D space so that they are culled correctly.  Also added a more intuitive positioning method useful for flat screen displays as well as planetariums
 - Added a heuristic that sometimes filters out ESRI's "No data available yet" tiles and uses available lower resoltion tiles instead.  This does not seem to work in all cases, and when it does not work, the "No data available yet" tile will show up as before
 - Added the support for temporarily modifying mouse sensitivity when zooming.  The `Z` key will increase the mouse sensitivity while it is pressed down by a factor of 8, the `X` key will decrease the mouse sensitivity while it is pressed down by a factor of 2
 - Added shortcut to disable rendering on master node (Alt+R)
 - Introduced global and master rotation that modify the location of screen space items
 - Added a feature that will check for a new released version at program start and provide information to the user in the lower right part of the screen and it will also enter a line into the log file
 - Added more statistics for the dashboard framerate items showing the extremes, standard deviation, etc

### UI Improvements
  - Added a panel for controlling the new session recording feature
 > To record a playback feature, you enter a filename and hit the `Record` button.  If you want to edit the recording afterwards, enable the `Text file format`.  The recording is stored in the `recording` directory by default, which can be changed in the `openspace.cfg`.  To play back a recording either select it in the dropdown menu or enter the name of the recording file in the text file and press `Play`
- Easy access settings panel for Renderables.
> Each scene graph node in the `Scene` menu now has a wrench icon next to it which will cause a panel for that scene graph node to pop out and be separately available until it is closed by the user.  Additionally, the top of the `Scene` menu now always contains the settings for the current focus node.  If this element is popped out, it will dynamically update if the current focus node changes
- Quick Enable feature for Renderables and Globe layers.  All renderable objects and layers on globes now have a checkbox with which the object can be quickly enabled or disabled without needing to open the submenu
- Visual indicator for enabled globe layers.  If a globe layer is enabled, its text will be rendered in green;  if it is not enabled, the text is white
- Sorting of Elements.  All elements in the UI are now correctly sorted;  either by adhering to the GUI sorting as specified in an asset file, or sorting the planets by the their distance from the Sun
- Improved scene menu search to make it possible to better search for objects that contain multiple words
- Scene pane saves state between uses.  When closing the `Scene` menu, the state of the tree will now be saved and not be closed when the menu is brought up again
- Improved display of scene shortcuts.  The list of available shortcuts are not presented in a more cohesive way to make them easier to access
- Visual improvement of fonts rendering.

### API
 - Updated GDAL version to 2.4.1
 - Finding configuration file now starts from the `bin` folder and continues upwards, rather than the current working directory as before
 - Add `asset.filePath` to asset API which contains the full path to the currently evaluated asset, enabling more useful error messages
 - Added the ability to query the OpenSpace documentation via the networking API
 - Added the ability to pass arguments to Lua scripts via JSON through the networking API
 - Added the ability to transport return values from Lua scripts back to the networking API clients
 - Added the ability to remove scenegraph nodes based on regular expressions

### Content
 - Added a new WMS layer for Mars containing >500 local HiRISE patches, served by ESRI
 - Added a new scene showing the trajectory of Apollo 8, and adding many new features to the various Apollo landing sites
 - Added a new scene containing the Insight lander.  The scene contains a model of the lander, its trajectory during entry into the Marsian atmosphere and the eventual landing.  The model changes throughout the different phases of the landing by showing, for example, the separation of the heat shield and the deployment of the parachute
 - Added new feature to show planetary surface labels.  Every major object in the Solar System, except for Earth, now has planetary labels that can be shown interactively.  The labels are taken from the database of USGS
 - Added a scene showing the Gaia mission using a new and experimental multiscale renderer.  The dataset that is automatically synchronized at startup only contains a few million stars for which the radial velocity is available.
 - Added grids for showing light days, light months, light years, and more.  These grids can be used to show the increasing scale when leaving the solar system
 - Added the trails of the Pioneer 11 and 12 missions as they were leaving the solar system
 - Added new SPICE kernels to the Juno scene to complete its coverage
 - Added Apogee and Galah gaia subsets rendered with the new star rendering method, howing the metal abundances in a subset of stars close to the Sun
 - Small fixes to the Messenger scene
 - Added WMS layer for Enceladus, Titan, and Europa
 - Added a spherical grid representing the Oort cloud

### Content Creation
 - Introducing a new base asset/scene that should not be directly loaded, but that can serve as a base for all other scenes.  This scene sets up default keybindings, loads the common content of the solar system and the digital universe, loads the Web UI, and configures globe browsing customizations
 - Added the ability to create custom focus nodes on planetary surfaces from Lua that can serve as a focus node for specific surface positions, such as Mars HiRISE patches, landing locations on the Moon, and others
 - Added a new Translation lcass that uses longitude/latitude information to position an object on a globe
 - Added Lua function to query property identifiers
 - Added example assets for some components

### Bugfixes
 - Fixed issue in which scene graph transformations were applied in the wrong order leading to strange results
 - Fix for a bug where the resolution of the globe layers would decrease when enabling a layer on some graphic cards
 - Fixed an issue where the loading screen would not show percentages when downloading files
 - Fixed an issue where the time notifier in the UI is not updated if the scene is paused
 - Fix for a bug where temporal WMS datasets would not be cached correctly
 - Fix a bug where the `H` key would not correctly show the trails again after hiding them
 - Correctly sort scene items in the Web UI
 - Fixed issues preventing multiple properties from being set simultaneously from a Lua script
 - Fix for bug where the global black-out would not work correctly
 - Only show screenspace renderables on non-UI windows 
 
### Optimizations
 - Increased rendering speed of Web UI
 - Slightly improved the rendering speed of globerendering
 - Slightly improved the rendering speed of the stars


# Beta-3 [0.13.0]
 - Version: 0.13.0
 - Date: 2018-11-05
 - Finished: [8e93463c1aba03445804c10172c85be69cbc1cb3](https://github.com/OpenSpace/OpenSpace/commit/8e93463c1aba03445804c10172c85be69cbc1cb3)

## Changelog
### Features
  - New CEF-based user interface (currently only on Windows)
  - Added shortcuts menu to execute Lua scripts without needing to be bound to keyboard keys
  - Updated GDAL to 2.3.2
  - Show percentages and progress for sync downloads
  - Added abililty to interpolate time for smoother time jumping
  - Ability to filter scene graph objects based on time
  - Additional lighting options for model rendering
  - Render on-screen text informing the user of ongoing application shutdown
  - Added ability to disable the console key for kiosk mode
  - Improved the tracking of the touch interface and made it easier to open the menu in a touch environment
  - Enable Spout texture sharing on default on Windows
  - Added Lua functions to print cluster id
  - Added configuration file that supportes spherical mirror configuration

### Content
  - Add a default path (`OpenSpace/../OpenSpaceData`) to search for planetary patches
  - Add a proper radiosphere that grows in real time
  - Add Hyperion and Mimas to Saturn's major moons
  - Enable the ability to not load an asset on default and later load it at runtime
  - Added simple example for a slide deck state machine
  - Added new dashboard item that shows the camera's current velocity
  - Add a new scale that changes its value based on the current time, reference time, and speed
  - Add a rotation that provides a static rotation based on in-game time
  - Simplify specification of opacity for text labels
  - Converted all images from using pbm format to png format for better compatibility
  - Add non-SI units to the distance conversion

### Bugfixes
  - Fixed bug causing incorrect aspect ratio for manually specified window sizes
  - Fix bug preventing specification of easing functions for property setting
  - Fixed focus node creation for local surface patches
  - Workaround for MacOS Mojave 10.14 where the rendering would only show up after the window has been moved

### Optimizations
  - Major improvement of planetary rendering performance
  - Improvements of atmosphere rendering performance
  - Improved application startup time
  - Better reuse of shader objects to reduce memory footprint
  - Better reuse of textures to reduce memory footprint
  - Better reuse of vertex buffer objects for Digital Universe dataset to reduce memory footprint
  - Improved rendering times by reusing uniform locations

# Beta-2 [0.12.0]
  - Version: 0.12.0
  - Date: 2018-07-11
  - Finished: [c2b1a3fd42b107ed37a1d0006058ae9d2df4baaf](https://github.com/OpenSpace/OpenSpace/commit/c2b1a3fd42b107ed37a1d0006058ae9d2df4baaf)

## Changelog
### Features
  - A pre-build binary for MacOS is included in the download section of the webpage
  - Added support for using joysticks and gamepads as input devices. The `data/assets/util/default_joystick.asset` controls the handling of connected joysticks
  - Bittorrent-based file synchronization has been completely removed in favor of HTTP-based synchronization. This change will fix the majority of issues that users had while synchronizing data in a firewalled environment
  - The `default.scene` will now by default start at "yesterday"s date and show the as-of-yet incomplete VIIRS image for "today" if the user jumps to "today"
  - The startup and shutdown times of the application has been overall lowered
  - **Potentially breaking change:**  The layout of the central `openspace.cfg` has been changed and users must adapt their old, modified variants for this release.  Mitigation consists of removing the `return {` and single `}` at the top and bottom of the file respectively
  - Added a mechanism to pass commandline arguments to OpenSpace that modify the loaded `openspace.cfg` to enable the setting of start-up scenes, SGCT configuration files and others from the commandline for clustered environments
  - When `PRINT_SCREEN` is creating a screenshot, it is now placed in the `screenshots/{current date}/` folder, rather than the `bin` folder as it was before
  - The default horizontal field-of-view has been changed to 80 degrees, which can be overwritten in the `openspace.cfg` file by the user by modifying the `sgct.config.single` parameters as described in the `scripts/configuration_helper.lua` file
  - When running OpenSpace in a windowed setup, manually changing the size of the window will now automatically adapt the aspect ratio that is used for the rendering
  - Added an inituial ability to automatically create focus markers on planets based on available `.info` files by editing the `data/assets/customization/globebrowsing.asset` file and changing `CreateFocusNodes` to `true`
  - Added the ability to use a single-file HTTP-based synchronization from third party locations. Examples of this are in the `data/assets/examples/urlsynchronization.asset`
  - It is now possible to zoom by using the left mouse button and pressing the Alt key in addition to using the right mouse button to support MacOS touch pads
  - Made it possible to click on the friction markers in the image to toggle the individual friction modes in addition to using the `F`, `Shift+F`, and `Ctrl+F` keyboard shortcuts
    - The `Global Properties -> Dashboard` now has a single property that will toggle its visibililty on screen
  - **Potentially breaking change:** The names of properties in the scene tree is now simplified and users must adapt their custom scripts to add a `Scene.` prefix to properties that change attributes of objects in the scene graph.
  - Added support for stb_image-based texture reader on non-Windows platforms

### Content
  - Added asset for the Messenger mission
  - Added Pluto to the default scene
  - Added Scaling node to all planets

### Bugfixes
  - Make the minimum skirt length of globes depenent on its radius to support small globes, such as moons of Mars, Jupiter, and Saturn
  - Fix bug preventing Saturn's rings from rendering
  - Fix bug causing Kepler-based translation to use a wrong value for the semi-major axis

# Beta-1 [0.11.1]
  - Version: 0.11.1
  - Date: 2018-02-13
  - Finished: [a65eea61a1b8807ce3d69e9925e75f8e3dfb085d](https://github.com/OpenSpace/OpenSpace/commit/a65eea61a1b8807ce3d69e9925e75f8e3dfb085d)

## Changelog
 - Changed default timeout to WMS servers from 5 minutes to 3 seconds, fixing a timeout wait on startup
 - Fixed hanging torrent download issue
 - Bugfixes and performance improvement for atmosphere rendering
 - Stability fixes with regard to caching
 - Updated H2 regions to a new dataset
 - Added spherical grids to Digital Universe dataset
 - Improve the texture quality by using Linear Mipmapping on default
 - Automatically compute a reasonable aspect ratio for custom window sizes
 - Fix issue with commandline arguments not being parsed
 - Fixed rendering issue where the stars would not show up if they are the only Digital Universe object included in the scene
 

# Beta-1 [0.11.0]
  - Version: 0.11.0
  - Date: 2018-01-01
  - Finished: [6e969794638d7e4761180dc97ca01fb35f356e46](https://github.com/OpenSpace/OpenSpace/commit/6e969794638d7e4761180dc97ca01fb35f356e46) 

## Changelog
### Content
  - Enabled atmospheric scattering around planets
  - Added Digital universe datasets (https://www.amnh.org/our-research/hayden-planetarium/digital-universe)
  - Mars
    - Added WMS server for color map
    - Added WMS server for MOLA hillshade
    - Added Phobos and Deimos
  - Earth
    - Added new ERSI high resolution dataset
  - Added scene for Voyager 1 and Voyager 2
  - Added minor moons for Jupiter, Saturn, Neptune, Uranus

### Features
  - Rendering methods
    - Added ability to provide rendering to Spout clients (spout.zeal.co)
    - Added configuration file for Spout cube output for use in Worldviewer (https://www.elumenati.com/product/worldviewer/)
    - Added projection method for Spherical mirrors (paulbourke.net/dome)
  - User Interface
    - Added on-screen information about friction status
    - Added automatic fading of objects based on distance
    - Improved informational text telling the user that a shutdown is imminent
    - Added TUIO touch interface implementation (https://www.tuio.org)
    - Added MacBook touch bar items for opening GUI and focussing on objects
    - Improved tooltip handling
      - Only show tooltips after one second of hovering
      - Added ability to disable tooltips
    - Enabled the manual sorting of items in the user interface
    - Added simplified GUI mode and shifted GUI activation keys (F1 -> F3  and F2 is new simplified GUI)
  - Content
    - Improved the behavior of billboard sizes by limiting minimum/maximum size
    - Added Loadingscreen to appear while a scene is loading
    - Added implementation to allow scenes to load multithreaded
    - Added Rotation method that stays fixed to a specified body
    - Added transformation objects that evaluate Lua scripts for rapid prototyping
    - Enabled multiple directories for image sequences like New Horizons and Rosetta
  - Scenes
    - Changed data layout by splitting old data/scene folder into data/asset and sync folders, thus separating the scene specification and the downloaded data
    - Added ability to execute global initialization scripts
    - Moved VRT specification into separate customization asset
    - Cleanup of Earth, Moon, and Mars WMS configuration files
  - Other
    - Made OpenSpace an AppBundle on MacOS
    - Set default number of antialiasing samples to 4
    - Cleanup of logging behavior
    - Added GIT commit hash output in log

### Bugfixes
  - Changed the default length of Uranus to prevent SPICE errors that would case Uranus' trail to query positions before 1850
  - Fixed bug that prevented separate GUI window from working
  - Added support for multiple ImGUI contexts used for multiple windows
  - Prevent crash from happening when too many texture units are requested
  - Fix Rosetta scene and rendering on MacOS
  - First steps towards making OpenSpaceEngine resilient against missing SGCT configuration errors

### API
  - Added ability to query the current binding of keys
  - Added ability to change the range of the delta time slider
  - Added ability to specify exponents for all numeric sliders
  - Added function to unload Mission file
  - Renaming path tokens
    - `${BASE_PATH}` -> `${BASE}`
    - `${OPENSPACE_DATA}` -> `${DATA}`
    - New token `${WEB}`
  - Redesigned on-screen text information to be more flexible

# Prerelease 15 (ASTC)  [0.10.0]
  - Version: 0.10.0
  - Date: 2017-10-24
  - Finished: [50fd93](https://github.com/OpenSpace/OpenSpace/commit/50fd9309ba9dc9e5d73bf4bde3b0d6014bb75287)
