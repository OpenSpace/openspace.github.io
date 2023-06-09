---
title: Satellites
layout: default
grand_parent: Users
parent: Content
nav_order: 2
---


## Satelllite Data from Celestrak
The satellite data included in OpenSpace comes from service [Celestrak](https://celestrak.com/), and in particular their current data page: [https://celestrak.com/NORAD/elements/](https://celestrak.com/NORAD/elements/). On this page, you will find overall categories in **BOLD** and their sub cateories listed below them. Listed below are the OpenSpace assets files that correspond. Should you wish to include an entire category, there are asset files to include named *satellites_communications*, *satellites_debris*, etc. The OpenSpace category of **Misc** corresponds to the first Celestrak category 'Special-Interest Satellites'.


## Satellites in the 'default' Profile

Satellites in the default scene can be activated with the 's' hotkey, or the 'Toggle Satellites' shortcut. They can also be found in the Scene menu under Solar System->Planets->Earth->Satellites. Below is a listing of the ones included in the default scene.

| Menu name | Celestrak category | Description |
| --- | ----------- | ------- |
| geo | Active Geosynchronous | Satellites that currently active and in a Geosynchronous orbit, meaning their orbital period matches Earth's rotation. |
| gps-ops | GPS Operational | The GPS satellites that give us our precise locations back here on Earth. |
| ISS | N/A | In this sub category you will find the model and the trail for the ISS. The trail for the ISS is the same data that can be found in the stations category. |
| stations | Space Stations | A collection of space stations (Including the ISS and China's Tiangong), along with certian cubesats and satellite constellations from space agencies. |
| tle-new | Last 30 Days' Launches | All the satellites that have been launched in the last 30 days. |
| visual | 100 (or so) Brightest | The 100 (or so) satellites that will appear brighest when viewed from Earth. |


## All Satellite Categories and Assets Included in OpenSpace
As mentioned above, satellites are grouped by categories and sub-categories that are created by CelesTrak.com. Below is a current listing of the ones included in OpenSpace:
### Communications
amateur
experimental
geostationary
globalstar
gorizont
intelsat
iridium
iridium_next
molniya
orbcomm
other_comm
raduga
ses
### Debris
debris_asat
debris_breezem
debris_fengyun
debris_iridium33
debris_kosmos2251
### Misc
brightest
cubesats
iss
military
other
radar
spacestations
tle-new
### Navigation
beidou
galileo
glosnass
gps
musson
nnss
sbas
### Science
education
engineering
geodetic
spaceearth
### Weather
argos
dmc
earth_resources
goes
noaa
planet
sarsat
spire
tdrss
weather


## Additional Features
See the Components/Satellites [page](/docs/components/satellites) for more detailed information and advanced usage of satellites in OpenSpace.
