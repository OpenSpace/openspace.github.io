---
title: Gaia
layout: default

parent: Content
nav_order: 4
---

This guide will explain how to render stars released by ESA's Gaia mission as their second data release (DR2) without having to create any subsets yourself.
If you are interested in advanced usage of the Gaia data, see [this page](../../components/gaia).

## 1. Define which scene to run
OpenSpace has several different scenes depending on what you want to show.  To change scene open openspace.cfg in a text editor and make sure that `Asset = "gaia"` is the only `Asset` line that is not commented-out.

To change anything in the scene go to data/assets/gaia.scene. Any of the following Gaia content can be enabled/disabled with by adding `--` in front of the corresponding line.
```
asset.require('scene/milkyway/gaia/gaiastars')
asset.require('scene/milkyway/gaia/apogee')
asset.require('scene/milkyway/gaia/galah')
asset.require('scene/solarsystem/missions/gaia/gaia')
asset.require('scene/solarsystem/missions/gaia/trail')
```

## 2. Run OpenSpace
When running OpenSpace there are several properties that you can change during runtime. In the GUI menu, expand Milky Way > Gaia Stars. The most important menu items are the following:

### File Path
This is used to change dataset during runtime.

### Render Option
There are 3 different render modes;  _Static_, _Color_ and _Motion_.  _Static_ uses only the position of the stars and assume that they all have the same magnitude.  _Color_ uses position, absolute magnitude (to calculate luminosity and apparent magnitude) and color.  _Motion_ adds velocity to the mix.  For a realistic rendering use _Color_.  To be able to make the stars move use _Motion_.

### Shader Option
Sets which technique to use for the rendering.  This will change what other options that will are available in the menu.  Generally _Points_ are faster than _Billboards_, especially for big datasets, and _SSBOs_ are faster than _VBOs_.  _SSBOs_ are not available for Mac users unfortunately. 

### Thresholds
Used to filter the data in real-time.  Sets min and maximum.  If they are set to the same value only that value will be filtered away.

### Rendered stars
The number of stars that are actually rendered on screen.

### Luminosity multiplier
Used to scale the brightness of the stars.  Good to use when traveling further out. 

### LOD Pixel Threshold
Turn this up to use LOD data.  Not necessary for small datasets (as the RV dataset) but a must for larger ones.

### Max GPU Memory
This determines how much memory we can use on the GPUs for our buffers.  If nothing is visible and the framerate drops to below 5 fps then try to decrease this value.  When rendering large datasets and the _GPU Stream Budget_ is down to 0 is may also be a good idea to try to increase this value.  Every GPU can allocate different max sizes so it is a matter of trial and error for every new hardware.  When you have found the maximum for you computer you can store that value in `gaiamission.asset` so it will be used on startup the next time.

### Filter Size & Normal Distribution Sigma (for _Points_ Shader Option)
These determine the size and form of the stars when one of the _Points_ shader options is selected.  A bigger filter size will decrease the performance.

### Billboard Size & Close-up Boost Distance (for _Billboards_ Shader Option)
These change the size when one of the _Billboards_ shader options is selected.  A larger size will decrease the performance here as well.
