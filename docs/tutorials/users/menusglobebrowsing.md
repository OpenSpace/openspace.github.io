---
title: Using the menus - GlobeBrowsing
layout: default
parent: User Tutorials
grand_parent: Tutorials

has_children: false
has_toc: false
nav_order: 6
---



# Using the Menus - Globebrowsing
{: .no_toc }

This section will cover the functionalty available when exploring worlds in the Solar System.

1. TOC
{:toc}

## Globe Properties
 - As with anything, Globe's have their own specific properties under their 'Renderable' section in the Scene menu. 
 - Their are many infrequently used settings, so only the most used ones will be desribed:
    - '_Labels_' - Some globes have labels which can be turned on or off. Labels are a sepecial property of a Globe and have their own internal properties.
    - '_Layers_' - Layers will be described in the next section of this page.
    - '_Perform Shading_' - This setting will darken the Globe based on the Sun. See [Lighting Conditions](#lighting-conditions) for more details.
    - '_Use Accurate Normals_' - Used in conjunction with the '_Perform Shading_' setting, this setting will use the enabled 'Height Layers' to further adjust the lighting conditions.
    - '_Eclipse_' - To see an eclipse happen on a globe, you must enable this setting.
    - '_Eclipse Hard Shadows_' - Used with the '_Eclipse_' setting this setting will disable the smoothing at the edges off the eclipse sections.
    - '_Target level of Detail Scale Factor_' - This setting will adjust the level off detail that is loaded for maps in relation to the distance to the camera. 
        - Lower values will make the map load faster, and give better performance, at the cost of map resolution.
        - Higher values will take longer to load and give worse performance, but will give a more detailed overall image.

## Layers and Their Settings
 - Without layers, the globe would be just a gray spheroid.
 - The layers of a globe are organized in to categories. 
    - '_ColorLayers_' are used to add maps and other visual information to the globe.
    - '_HeightLayers_' are used to deform the globe, sometimes refered to as a _Digital Elevation Model_
    - Some globes will have other special groups such as '_Overlays_' or '_WaterMasks_' on earth.
 - The layers of a globe can be turned on or off by using the checkbox next to their name.
    - Enabled layers will be tinted with the highlight color.
 - Aside from enabling and disabling a layer, you can open its internal menu to adjust the settings off a layer. 
    - For ColorLayers, use the _Opacity_, _Gamma_, and _Multiplier_ settings to change the way the layer appears:
    - For HeightLayers, use the _Gamma_ and _Multiplier_ settings can be used to exagerate the elevation, however this can lead to unexpected rendering issues.
    - For HeightLayers, the _Offset_ can be used to elevate one heightmap relative to another.

## Layer Ordering and Blending
 - The order of the layers of a globe in in the menus, represents the order that are wrapped over the globe, like the layers of an onion.
 - The last layer in the menu list will appear as the outter most layer off the globe where as the first would be the inner most layer.
 - If multiple global layers are enabled, only the outter most one will be visible.
 - This becomes important when combinging different maps which that are color/monochromatic or global/regional.
 - If a layer is monochromatic, its '_Blend Mode_' can be set to '_Color_' and it's pixels will inherit the color values of the layer underneath it. 
 - Regional layers must appear lower in the menu then global layers in order to combine them.

## Lighting Conditions
 - By default globes will have the '_Perform Shading_' setting enabled, and thus will be lit based on their rotation and position relative to the Sun.
 - In order to light a different part of the globe, change the simulation time.
 - For times when you don't want to change the simulation time, you can disable the '_Perform Shading_' property of the globe.
 - If you want the globe to be even brighter even when not shaded, try increasing the '_Multiplier_' setting of the inner most layer as described above.

## Atmospheres
 - Venus, Earth, Mars and Titan have an atmosphere attached to their globe.
 - The atmosphere is a seperate item in the 'Scene' menu from the globe itself.
 - The atmoshpere will affect the lighting conditions on the globe, even if 'Perform Shading' is not enabled.
 - In order to always have the are of the globe you are looking at lit with an atmosphere enabled, you must enable the '_Enable Sun on Camera Position_' setting for the globe's atmosphere along with disabling the '_Perform Shading_' setting on the globe.
 - The only other common settings to change in an atmosphere would be '_Enable Hard Shadows for Eclipes_' when you are trying to visualize an eclipes, or '_Sun Intensity_' if you wish to brighten or dim the overall lighting of a globe.

## Special Layers on Earth
 - The default layer on Earth is a special "combo layer", this means that it is actually two layers that will fade from one to the other based on a specific tile level. The "_ESRI VIIRS COMBO_" fades between the "_VIIRS SNPP (Temporal)_" layer and the "_ESRI World Imagery Layer_"
 - Earth has special layers in the "Overlay" group that show country features/names, coastlines and more.  
 - Earth has a special NightLayers group since we create light that is visible on the dark side off the planet.
 - The portion of the Earth that would be darkend by the '_Perform Shading_' section is instead rendered with a differnt map depecting the city lights.
 - If you wish to show a fully lit earth at any simulation time, you must disable any night layers.

## Video

<iframe width="740" height="530" src="https://www.youtube.com/embed/Bx_urBYAEqA" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

| Video time | Description |
|:-------------|:------------------|
| 0:00 | Moon - Perform shading. |
| 0:22 | Moon - Use accurate normals |
| 1:39 | Moon - Labels |
| 2:24 | Moon - layers color/height. |
| 3:51 | Earth - Default combo layer |
| 4:57 | Earth - Temporal layers |
| 6:03 | Earth - Night layers |
| 6:38 | Earth - Overlays |
| 7:30 | Mars - Atmosphere lighting conditions |
| 8:24 | Mars - Layer settings |
| 9:49 | Mars - Layer blending options |

---
<span class="v-align-middle">
[Using the Menus - Datasets](/docs/tutorials/users/menusdatasets){: .btn .btn-purple }
</span>
<span class="fs-6"><-- Previous |</span>
<span class="fs-6">Next -->  </span>
<span class="v-align-middle">
[Coming Soon](/docs/tutorials/users/menusglobebrowsing){: .btn .btn-purple }
</span>

