---
title: Small Solarsystem Body Database
layout: default

grand_parent: Builders
parent: Ephemeris
nav_order: 3
---

This page covers the basics of downloading orbital data for a solar system object in the proper format required by OpenSpace, and then configuring a renderable scenegraph node for it.

This method differs from the JPL Horizons [page](horizons-web) in that it provides parameters that describe the orbit of an object rather than its pre-computed coordinates.  This SBDB method is best for objects that have stable, predictable orbits.

# Downloading Orbital Data from the JPL Small-Body Database (SBDB)
Browse to the JPL SBDB query page [here](https://ssd.jpl.nasa.gov/sbdb_query.cgi) and follow the instructions for each input section below.

## Search Constraints
There are currently just under one million Small SolarSystem Bodies (SSSB) listed in this database.  Attempting to render all of them at once would cause low rendering performance and result in "visualization overload," so some level of filtering is necessary.

Under the **Step 1** header, there are a number of filtering options.  Asteroids or comets can be selected, as well as sub-groups within those classifications (e.g. main asteroid belt).  At the bottom of this section, additional filtering can be applied using object characteristics.  For example, objects of a certain size, orbital period, or inclination can be selected and combined with a logical AND/OR operation.

## Output Fields - **Step 2**
Select oribtal elements in the **Step 2** section in the fields selections below.  Do not select any of the "Pre-defined field sets"

### Object Fields
Select only **object full name/designation**

### Orbital and Model Parameter Fields
Multi-select (CTRL+mouse clicks) the following fields:
- **epoch of osculation in calendar date/time form (TDB)**
- **[e] eccentricity**
- **[a] semi-major axis (au)**
- **[i] inclination; angle with respect to x-y ecliptic plane (deg)**
- **longitude of the ascending node (deg)**
- **argument of perihelion (deg)**
- **[M] mean anomaly (deg)**
- **sidereal orbital period (d)**

## Output Fields - **Step 3**
Click the **Append Selected** button, at which point a list will appear with labels for steps 4 and 5.  Verify that the list contains *only* these elements *in this exact order* (use the up/down buttons to adjust the order if necessary):
- **object fullname**
- **epoch (TDB)**
- **e**
- **a (au)**
- **i (deg)**
- **node (deg)**
- **peri (deg)**
- **M (deg)**
- **period (d)**

## Format Options
Select the **CSV download** option, and then click the **Generate Table** button.  The .csv file will then be automatically downloaded by the browser.

# Data Usage
This wiki covers the scenario where an asset file references a data file served by one of the OpenSpace sync servers.  At runtime, the file will be downloaded if a local copy does not already exist.  This requires the file generated in the above steps to be uploaded to an OpenSpace sync server by one of the project's server administrators.

For testing purposes, the file can be included in the asset by using the `localResource` method, but this is not discussed here.

# Create an Asset File
The following is an example from the `solarsystem/sssb/pha.asset` file that is currently included in the latest OpenSpace release.  This asset renders the asteroids that have been flagged in the JPL database as being **A**steroids which are **P**otentially **H**azardous (PHA) to Earth.
```
local assetHelper = asset.require('util/asset_helper')
local sharedSssb = asset.require('./sssb_shared')

local filepath = sharedSssb.downloadSssbDatabaseFile(asset, 'pha', 'sssb_data_pha')
local object = sharedSssb.createSssbGroupObject("sssb_data_pha.csv", filepath, { 0.75, 0.2, 0.2 })
object.Renderable.Enabled = false

assetHelper.registerSceneGraphNodesAndExport(asset, { object })
```
The `util/asset_helper` file provides utilities and is included in almost all assets.  The `sssb_shared` file provides the functionality necessary to configure the object in a format that can be interpreted by OpenSpace as a scenegraph node.

The `downloadSssbDatabaseFile` function sets up a reference to an http-synchronized file which will be downloaded from the sync server mentioned previously.  The 2nd argument is just a name, but the final argument needs to match the corresponding entry stored at the sync server.  The `createSssbGroupObject` is also provided by the `sssb_shared` file, and it creates a Lua table in the format expected of a scenegraph node.  T he 1st argument is the exact filename that will be stored in the local sync folder as a result of the download step above.  The final argument is the RGB color of its orbital trail.

In this example the renderable will not be enabled by default, but can of course be enabled manually in the GUI or console.  As the function name implies, the final call to `registerSceneGraphNodesAndExport` completes the process and registers this asset as a scenegraph node in OpenSpace.

# Add the Asset to OpenSpace
The final step is to simply add this asset to OpenSpace for rendering.  This can be done by either:
1. Including the asset in a **.scene** file before starting OpenSpace:
`asset.require('scene/solarsystem/sssb/pha')`
2. Typing in the **\`** console while OpenSpace is running:
`openspace.asset.add('scene/solarsystem/sssb/pha')`
