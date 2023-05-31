Please note: The following release notes are incomplete and will be updated as the release candidate evolves.

# Features
 - Add settings in OpenSpaceEngine that sets visibility in gui / Adapt the visibility settings for all properties / Add the ability to set the default property visibility in the openspace.cfg file, which can be overridden with the OPENSPACE_LEVEL environment variable
 - OpenSpace/feature/documentation-overhaul #2604
 - OpenSpace/feature/video-module #2608
 - Feature/geojson (#2595)
 - feature/missions #2603
 - feature/getting-started-tour (#2189)
 - Fading of propertyowners through GUI, and more owners with fade property (#2557)
 - Add ability to cache globe data using MRFs (#2565)
 - Add the ability to jump to a path endpoint #2568
 - Automatically abort ongoing shutdown when interacting with the mouse or the keyboard (closes #2393)
 - Adding option for constant velocity flight (closes #2150)
 - Limit min/max distance #2570
 - Optimizations for RenderableTrailTrajectory
 - Add option to invert idle behavior, Both through separate property and by allowing negative speed factor (fixes #2379)
 - Add new configuration file that also adds graphics to the UI window (closes #2530)
 - Touch module code cleanup. Remove unused feature that allowed us to "pick" nodes using touch (it didn't really work and had some nasty hardcoded and costly implementation). Fixes Touch interaction picking refactor #1041 (#2465)
 - Sort actions based on their name or their identifier if the names don't exist
 - Add option to HttpSynchronization to automatically unzip downloaded files (closes #1852)
 - Make it possible to set the WebGUI port from the openspace.cfg file (closes #2279)
 - Add the ability to Skybrowser images for drag and drop
 - Add property to disable all mouse input in OpenSpace engine (#2361)
 - Improve SkyBrowser performance
 - Add property to disable zoom and roll interaction for touch
 - Add the ability to disablee keybindings (closes #2238)
 - SkyBrowser: Being able to make the image inset with a rounded corner #2029
 - Expose ambient intensity value for globes as a property
 - Enable highlights in grids (#1683)
 - Add ability to select constellations (#1682)
 - SkyBrowser Hash Handling. Add the loading of a hash for wwt image files and automatically force a redownload of the files if the hash has changed. Move the wwtdataimages location into the sync folder (#2201)
 - Feature/satellites (#2185)
 - Expose the SGCT statistics information through a property in the RenderEngine (closes #2195)
 - Fade out renderables in atmosphere
 - Add enable/disable property for TimelineRotation (#1607)
 - Update Spice repository
 - Add the ability to configure the Console key through the openspace.cfg (closes #2573)
 - Add a message that we are running a debug build to the version information (closes #2523)


## Launcher
 - Allow Window Config GUI to Edit Files (#2574)
 - Increase the size of the configuration boxes in the launcher (closes #1785)
 - Allow the ScriptlogDialog to return multiple scripts; Make use of the Dialog in the Properties panel (closes #2253)
 - Replace profile actions/keybind editor button with single close button (#2497)
 - Rename "Keybindings" panel to "Actions & Keybindings" (closes #2363)
 - Add the ability to open a different scriptlog file when changing the additional scripts (closes #1545)
 - Add info tooltips to profile dropdown

# Content
## New Assets/Profiles
 - added scale objects (#2605)
 - added first amnh layers (#2612)
 - added triton voyager2 layer (#2611)
 - Add top dwarf planets #1712
 - Add Lunar Orbiter Mosaic layer
 - Artemis mission (#2597)
 - Updating SPICE Kernels and adding new Moons to Outer Planets (#2556)
 - Add new 99.5% coverage CTX layer
 - Add v3 WAC (#2555)
 - Add a new combined clouds-magellan layer for Venus (closes #1534)
 - Add combo layer that shows the NOAA20 VIIRS layer (closes #2538)
 - Add Ceres in dwarf planet folder (#2295)
 - Add an empty profile "empty.profile"
 - Add asset for Shepherd moon group of Saturn system (#2157)
 - Add Itokawa asset (#1264)
 - Add the JUICE mission (#2155)

## Updates to existing Assets/Profiles
 - Update some assets using Horizons data that have been updated (#2614)
 - Better organization for moons and some GUI Name fixes #2609
 - Constellations - Actions for zodiac constellations. #2272
 - Added action for global lighting of all globes (closes #2494)
 - Disabled assets for asteroids profile start (#2590)
 - Move the keybindings out of the base.asset and the specific label keybinding out of the default_keybindings
 - Switch MessengerTrail to RenderableTrailTrajectory in order to match start/end times, and add corresponding sample interval (#2552)
 - Update exoplanets data (#2450)
 - Update Juno kernels
 - Voyager assets now respects asset.enabled argument when it's passed in asset.require(). Added tags to Voyager models in assets
 - Add option to specify an offset distance for RenderableNodeLine (#2483)
 -  Issue/2408: Moving actions from profiles into assets #2491 
 -  Add actions for minor moons #2476 
 - Extended EndTime for Voyager 1 & 2 until 2300 so that trails are visible for longer.
 - Issue/1486: Create labels for all moons
 - Add lighthour grid to DU, and lightminute and lightsecond grids to Earth (closes #2439)
 - Move the Milky Way Image and arm labels from /Universe/Galaxies to /Milky Way
 - Remove luastatemachine example asset, closes #2193
 - Rename ISS scene graph node #2245 
 - Adds labels to the grids (fixes #1244
 - Add trail that co-revolves with L2 around the Sun. Also tweaking the trail colors and speeds in the timelapse script (#2220)
 - Update the Ipac example asset
 - More explanation of the static magnetosphere


## Content creation
 - Add the ability to pass a script to the setPropertyValue function that is called after interpolation has finished
 - Send the origin and the destination scene graph nodes along with the events signalling the beginning or the end of a camera path (closes #1834)
 - Add events when paths are started or finished (closes #1834)
 - Add the ability to start a profile paused (closes #2228)
 - Add a new dashboard item that shows the state of input devices (closes #2415)
 - Add new dashboard item to show elapsed times (closes #2234
 - Make the argument in asset.localResource optional. If nothing is provided, then the path to the current directory that the asset is located in is returned
 - Add the ability to pass a boolean value into the require function that gets passed into the loaded asset as a `enabled` property (#2187)
 - Add the ability to use integer NAIF IDs in a SpiceTranslation
 - Add property that contains the list of all compiled modules (closes #1021)
 - added events for when renderables are enabled/disabled that can be used to link renderables together (#2132)
 - Make it possible to individually set the base radius for RenderablePrism shape, The prism can now be a cone, a pyramid, or any other weird shape that you might want!
 - Add New function that resets screenshot index to 0. Usefull when capturing png sequence for video


### Lua
 - Add new Lua function that creates a valid identifier from any string
 - Add new Lua function to load CSV file,  utilize new function to correctly load , inside field values (closes #2124)
 - Updated documentation for setPropertyValueSingle with all avaiable easing functions
 - Add some helper scripts to modify property values (appendToList, add, invertBoolean)
 - Add lua functions to get distance to bounding and interaction sphere
 - Add Lua function to get current distance to focus
 - Add function to return a list of all tags
 - Add the ability to move globe layers based on their name (closes #2411)
 - Changes to addCustomProperty (closes #2433)
 - Add a lua function to target previous and next interesting anchor
 - Add Lua function that returns information about the current OpenSpace version (closes #2136)
 - Make it possible to trigger camera path with zero duration


# Bug Fixes
 - Feature/model-opacity #2550
 - Feature/touch fixes (#2463)
 - Multiple keys for same property in some assets #2598
 - Harmonize capitalization of action names (#2579)
 - Provide error message when running OpenSpace from a folder containing a ', ", [, or ] (closes #2563)
 - Issue loading mask file in sgct config #2370
 - Don't subsample the height map on planets (closes #2472)
 - Provide a proper error message when trying to overwrite a hidden profile (closes #2575)
 - Use correct FOV calculations to handle portrait or landscape windows (#2554)
 - Correctly parse SSSB files that use an integer epoch, rather than a floating point one (closes #2551)
 - Check for illegal keywords in the header of Speck files to detect invalid files (closes #2549)
 - Switch to std::list for adding & removing assets in deterministic order (#2543)
 - Fix Constellation selection doesn't apply to labels #2382
 - Add more description to the --config command
 - Only check major Horizons version for compatibility (closes #2507)
 - Prevent errors from settings asset when building without the touch module
 - Check for invalid indices in the Gaia stars to prevent crashes (closes #2495)
 - Prevent infinite loop when extracting invalid commandline arguments (closes #2349)
 - Improve behavior for gui window and separate render window (#2515)
 - Show error message when trying to save navigation state to an invalid file path (closes #2508)
 - Make the local bookmarks print their error message if they fail;  also replace whitespaces with underscores for identifiers
 - Provide informational text in the actions panel if the user tries to create an illegal identifier (closes #2289)
 - Fix drag-drop for the interesting nodes panel in the Launcher(closes #2346)
 - Fix  Property owners get wrong name in GUI #2521
 - DashboardItem now listens to paramter 'enabled' in constructor
 - Fix bug where triggering of action via keybinds didn't get called
 - Fixed bug where default value for 'element' in GPTranslation was seen as invalid.
 - No longer trigger an assert when binding a key to an action that does not exist (closes #2485)
 - Properly report an error when an .info file is missing the identifier, preventing the addition of a layer without one (closes #2490)
 - Remove unintentional default value for skybrowser/exoplanet module enabled property (closes #2464)
 -  GUI allows, and crash, when input field has NaN value #2452 
 - Fix issue with some action folder sin the Action panel not being clickable #2467
 - Also apply the RenderableTravelSpeed changes to the fadeLength parameter
 - Add special case to the string tokenizer for "Keypad +" (closes #2358)
 - Make the travel indicator take floating point length values smaller than 1 (closes #2459)
 - Fix for case-sensitive rainbowgradient.cmap file in sync dir
 - Correctly swizzle the textures for ScreenSpaceImage types to allow for 8 bit grayscale images (closes #2330)
 - Don't render RenderableTrailTrajectory if the time is _exactly_ the start time (closes #2314)
 - Add support for multiple occurrances of -c commandline argument
 - Use the et2utc function in case the normal date conversion fails
 - Fixed bug where lua function openspace.pathnavigation.isFlying() returned unexpected value.
 - Make the addSceneGraphNode call in the local bookmarks file protected (closes #1483)
 - Fix issue when providing a URL that ends in / in a UrlSynchronization(closes #2435)
 - Add support for adding StringProperty in addCustomProperty script
 - Prevent a crash in the SGCT Editor when trying to add more than 2 windows on a computer with only 1 monitor
 - Update xbox controller asset
 - Various precision fixes for camera paths (#2212)
 - Don't crash when trying to add assets with invalid path (closes #2299)
 - Ensure that image paths in the ImageSequenceTileProvider are sorted (closes #2205)
 - Fix for linux crashing when reading OMM files
 - Use Sun position instead of SSB in Sun light source (see #2223)
 - Fix collision between ImGui and WebGui
 - Remove legacy geometry specification from RenderablePlanetProjection (closes #1967)
 - Move the Lua Console updating into the actual postSyncPreDraw function so that it gets called accuratly when GUI windows are present (closes #2141)
 - Adapt the ImGui GIBS panel to the new tileprovider format (closes #2108)
 - SkyBrowser
   - Issue/2313: Ensure all nodes in a cluster loads the image collection in the sky browser
   - Fix sky browser space craft pointing
   - Fix bug that channels in cluster don't set the field of view to the same value after animating in SkyBrowser (#2425)
   - Fix bug for screenspace sky browser scale crash (#2280)
   - Skybrowsing: Fix bug when master has no rendering
   -  SkyBrowser scale sometimes doesn't update the border radius in time #2266 
   - SkyBrowser: Ensure browser is initialized properly before executing javascript
   - SkyBrowser: Make it harder to input wrong values
   - SkyBrowser: Fix bug of sending set radius message too early
   - SkyBrowser: Disable hover circle per default when setting renderable and throw warning if setting to non-existing node (fixes #2153) 

# Breaking Changes
 - Make the check for whitespaces and dots in identifiers fatal also in non-Debug builds
 - Provide error message if a GuiPath does not start with / ; Automatically add / in the Profile editor.  Default initialize all paths to / (closes #2318)
 - Remove Earth layers that no longer work







Star fadeout
The fading happens

    when you enter the atmosphere
    when you are in the sunny area of a globe

Properties for each atmosphere are

    The angle where the sunset starts
    The angle where the sunset ends
    The percentage of the atmosphere height where the fading should happen.

Before merge, there is one edge case that should be accounted for. It is if the camera is located in an atmosphere and then uses the flyToGeo script to fly somewhere else, the renderables are not faded in as the camera has not transitet the "fading section". This could be resolved by setting the fading coefficient to 1 in the beginning of each render loop




Feature/satellites (#2185)
* Remove planet geometry and simplespheregeometry
* Only use a single TLE loading implementation
* Add caching to the satellite loader;  Add Lua function to load kepler file
* Fix RenderablePlanetProjection specification
* Add OMM loading funtion;  Remove mean motion from Kepler parameters
* Replace TLETranslation class with GPTranslation and support OMM files
* Support loading SMDB files in kepler functions
* Merge RenderableSatellites and RenderableSmallBody with RenderableOrbitalKepler
* Update submodules
* Adapt existing satellites to new OMM file type
* Remove TLE helper
* Remove SSSB shared file and adapt sssb assets


Changes to addCustomProperty (closes #2433)
 - Don't create a Lua context for an empty onChange string
 - Add support for StringListProperty
 - Add documentation
 - Add error message when a type is not supported



MRF
   Enables globe-browsing data to be cached using caching mrf's as it is loaded from the original dataset. Subsequent reads of tiles that have been cached do not query the original dataset but picks it up from the mrf data.
   Supports anything that can be used a dataset for a gdal raster but raw images such as JPGs are explicitly disallowed as they lack necessary geotransform data.

   Activated on a global scale by setting the following keys in openspace.cfg (ModuleConfigurations/GlobeBrowsing)
     MRFCacheEnabled = true,
     MRFCacheLocation = "<somepath>",
   Settings can be overriden on a per-layer basis by adding the following entries to the layer entity of an asset
      CacheSettings = { Enabled = true, Compression = "LERC", BlockSize = 512, Quality=25 },

   The following per-layer settings are available and override the global module settings:
   Enabled : enable/disable caching for this layer.
   Compression: The compression algorithm to use for tile cache storage. (JPEG, PNG, or LERC)
   BlockSize: Size of tiles in cache, should be a multiple of 2 although this is not required.
   Quality: The quality setting of the JPEG compression (when used)

   Note that heightlayers must use LERC compresison and this is the default unless overridden by a layer.

GeoJSON
   - Add the option to add geojson components to globes, from geojson files. One geojson file creates one GeoJsonComponent, which in turn may contain multiple GlobeGeometryFeatures

   - Geojson is a format that supports points, lines, and polygons. In addition to the basic functionality, extra features have been added that will long-term allow rendering the geometry needed to represent KML files (another format for geospatial geometry data). Here are links to references for both formats:
     Geojson: https://geojson.org/
      KML: https://developers.google.com/kml/documentation/kmlreference

    data/assets/examples/geojson includes some example files that I have used for testing. Any geojson file can also be added through drag-n-drop. Note however that you might need to change the AltitudeMode or HeightOffset properties for the feature to be visible
