---
title: Exoplanets
layout: default
grand_parent: Users
parent: Content
nav_order: 2
---

## About the Exoplanets Module
The exoplanets module includes the possibility of adding visualizations of confirmed exoplanets and their host stars to OpenSpace. The data comes from the [NASA Exoplanet Archive](https://exoplanetarchive.ipac.caltech.edu) and includes a large range of properties on the exoplanet systems, often including uncertainty estimations. A table of the complete dataset can be found here: [Planetary Systems Coposite Data](https://exoplanetarchive.ipac.caltech.edu/cgi-bin/TblView/nph-tblView?app=ExoTbls&config=PSCompPars).

The visualizations are based on a thesis project done by Karin Reidarman in 2018.

## How to add an exoplanet system to OpenSpace
Exoplanet systems of interest must be added to OpenSpace individually. The reason for this is that it is impractical to load all the systems in the database into OpenSpace on start-up due to the large number of confirmed exoplanets.

Exoplanets can be added and removed during runtime through the Exoplanets GUI panel, with the symbol:  <img src="/assets/images/users/content/baseline_hdr_strong_black_18dp.png" alt="Exoplanets GUI Symbol" width="20em" height="20em">

It is also possible to add exoplanet systems before startup using the `openspace.exoplanets.addExoplanetSystem(name)` function in the OpenSpace scripting API, where the name of the system is the name of the host star. For example, `openspace.exoplanets.addExoplanetSystem("Kepler-11")` adds the Kepler-11 system, a system discovered in 2010 with a total of 6 confirmed orbiting the host star Kepler-11. It is also possible to add multiple systems at once by specifying a list of host names as input, for example like `{"Kepler-11", "GJ 1061"}`.

Added exoplanet systems can be found in the Scene GUI under “Milky Way → Exoplanets → Exoplanet Systems”.

## About the visualizations
The focus of the visualization lies on the composition of the exoplanet systems and the orbital properties of the planets, such as their eccentricity, semi-major axis and orbital period. The upper and lower uncertainty of the semi-major axis are also visualized, by a blue-green-red colored band around the orbit. The wider the band is, the more uncertain is the data on the semi-major axis of the orbit. 

In the cases when there is data on the radius of a star/planet, they are visualized by a renderable globe with a corresponding radius. The color of the star is also computed from its effective color, resulting in a blue-white-yellow-red color scheme from the hottest to coldest star. 
