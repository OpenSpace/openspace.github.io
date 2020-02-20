---
title: Horizons
layout: default

grand_parent: Builders
parent: Ephemeris
nav_order: 1
---

This covers the basics of downloading ephemeris data for a solar system object in the proper format for OpenSpace, and then configuring a renderable asset for it.  This document only applies to an object in the solar system, using the sun as the origin.

This method differs from the JPL Small SolarSystem Body Database ([SBDB page](sbdb)) in that it provides pre-computed positions in galactic coordinates in a specified time window.  The SBDB method provides orbital characteristics that are used to compute the position without a time window restriction.  Objects with irregular orbits must use this Horizons method.

# Downloading Ephemeris Data from JPL Horizons Site
Browse to Horizons page (https://ssd.jpl.nasa.gov/horizons.cgi).  Follow instructions for each input section below.

## Ephemeris Type
Click *change* and select **Observer Table**.

## Target Body
Click *change* enter the desired object identifier.

## Observer Location
Click *change* and type `@0` in the text entry box.  You should end up with`Solar System Barycenter (SSB) [500@0]`.

## Time Span
Click *change* and pick whatever time range you want.  Note that these depend on the target, and an error may result if no data exists in the specified range.

## Table Settings
Click *change* on **Table Settings**.  Only the following checkboxes should be selected:
```
20. Observer range & range-rate
33. Galactic longitude & latitude
```
For the optional settings at the bottom, use the following:

- date/time format = calendar date/time
- time digits = HH:MM:SS
- angle format = decimal degrees
- output units = km & km/s
- range units = kilometers
- refraction model = none
- (no values for the 5 cutoff variables)
- suppress range-rate = enabled
- skip daylight = disabled
- extra precision = disabled
- RTS flag = disable
- reference system = ICRF/J2000.0
- CSV format = disabled
- object page = enabled

## Display Output
Click *change* and select "plain text".

## Generate Output
Finally, click on the **Generate Ephemeris** button to get the ephemeris data in text format, and save to a **.dat** file.

# Examine Downloaded Output
Examine the .dat file and verify that it is valid.  If it only contains the header but no space-delimited lines of data, then there should be an error message explaining the problem.  For example, this will happen if the start/end dates are beyond the valid time range of the target object.

# Data Usage
This wiki covers the scenario where an asset file references a data file served by one of the OpenSpace sync servers.  At runtime, the file will be downloaded if a local copy does not already exist.  This requires the file generated in the above steps to be uploaded to an OpenSpace sync server by one of the project's server administrators.

For testing purposes, the file can be included in the asset by using the `localResource` method, but this is not discussed here.

# Create an Asset File
The following is an example asset file of the interstellar object 'Oumuamua.  This file is located at **data/assets/scene/solarsystem/interstellar/oumuamua.asset** in the OpenSpace directory structure.  This asset file will create a node (not renderable) for the position of the object, and a renderable trail.
```
local assetHelper = asset.require('util/asset_helper')
local sunTransforms = asset.require('scene/solarsystem/sun/transforms')

local trajectory = asset.syncedResource({
    Name = "'Oumuamua Trajectory",
    Type = "HttpSynchronization",
    Identifier = "oumuamua_horizons",
    Version = 1
})

local OumuamuaTrail = {
    Identifier = "OumuamuaTrail",
    Parent = sunTransforms.SolarSystemBarycenter.Identifier,
    Renderable = {
        Type = "RenderableTrailTrajectory",
        Translation = {
            Type = "HorizonsTranslation",
            HorizonsTextFile = trajectory .. "/horizons_oumuamua.dat"
        },
        Color = { 0.9, 0.9, 0.0 },
        StartTime = "2014 JAN 01 00:00:00",
        EndTime = "2023 JAN 01 00:00:00",
        SampleInterval = 7000,
        TimeStampSubsampleFactor = 1
    },
    GUI = {
        Name = "'Oumuamua Trail",
        Path = "/Solar System/Interstellar"
    }
}

local OumuamuaPosition = {
    Identifier = "OumuamuaPosition",
    Parent = sunTransforms.SolarSystemBarycenter.Identifier,
    Transform = {
        Translation = {
            Type = "HorizonsTranslation",
            HorizonsTextFile = trajectory .. "/horizons_oumuamua.dat"
        },
    },
    GUI = {
        Name = "'Oumuamua",
        Path = "/Solar System/Interstellar"
    }
}

assetHelper.registerSceneGraphNodesAndExport(asset, { OumuamuaPosition, OumuamuaTrail })
```
In this example, the position and trail use the sun's barycenter (from `sunTransforms`) as the parent observer.  The Horizons data file is included here as an `HttpSynchronization` synced resource with the `trajectory` variable.  The translation type is `HorizonsTranslation` which requires a `HorizonsTextFile` to be specified using the `trajectory` path from the asset mentioned above.  The renderable trail has a start & end time, with a `SampleInterval` value that divides the time range into a number of segments.

# Add the Asset to OpenSpace
The final step is to simply add this asset to OpenSpace for rendering.  This can be done by either:
1. Including the asset in a **.scene** file before starting OpenSpace:
`asset.require('scene/solarsystem/interstellar/oumuamua')`
2. Typing in the \` console while OpenSpace is running:
`openspace.asset.add('scene/solarsystem/interstellar/oumuamua')`
