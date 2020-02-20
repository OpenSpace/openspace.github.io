---
title: RenderableGlobe
layout: default

grand_parent: Developers
parent: Globebrowsing
nav_order: 1
---

# RenderableGlobe
The **RenderableGlobe** is the base of globe browsing.  This is a class that extends **Renderable** with all the features required for globe rendering.  It contains all the base properties for a globe together with its sub components.

## General Properties
  - **performShading** -- **Boolean** value determining if shading should be performed or not.
  - **useAccurateNormals** -- **Boolean** value determining if normals should be calculated in the fragment shader based on hight layers or if the normals should be approximated as the ellipsoid normals.
  - **lodScaleFactor** -- **Float** value determining the level of detail of the globe.  A lower value will decrease the number of rendered chunks and hence also the render time.  A high value will increase the detail level of the textures and the number of rendered chunks.
  - **orenNayarRoughness** -- **Boolean** value determining the roughness used in the Oren-Nayar BRDF.  Some surface reflections are better approximated using this diffuse BRDF.  For example, the Moon has a lot of crystal structures which reflects light differently than standard diffuse surfaces.  A high roughness for the Moon better represents the actual surface.  This implementation of the Oren-Nayar BRDF however seems to be non-energy conserving which means that the surface overall becomes darker for higher roughness.  This can be compensated using a higher multiplier for the color layers but should probably be looked in to in the future.

## Debug Properties
  - **showChunkEdges** -- **Boolean** value determining if edges of chunks are rendered or not.  Chunks that are rendered in model space have green edges while camera space rendered chunks have red edges.
  - **showChunkBounds** -- **Boolean** value determining if the bounding volumes of each chunk should be rendered.  Bounding volumes are octahedrons covering the chunk.  These are rendered in camera space using the debug renderer.
  - **showChunkAABB** -- **Boolean** value determining if axis aligned bounding boxes should be rendered for the chunks.  The AABBs are represented and rendered in camera space and used for frustum culling.  These are rendered in camera space using the debug renderer.
  - **showHeightResolution** -- **Boolean** value determining if height resolution should be rendered.  The height resolution is represented as dots positioned at each vertex that contains a new value in the height map.
  - **showHeightIntensities** -- **Boolean** value determining if height intensities should be rendered on top of color.
  - **performFrustumCulling** -- **Boolean** value determining if frutum culling should be enabled.
  - **performHorizonCulling** -- **Boolean** value determining if horizon culling should be enabled.
  - **levelByProjectedAreaElseDistance** -- **Boolean** value determining how the chunk level evaluation is performed.  Using projected area, generally fewer chunks are rendered decreasing render time.  The downside is that blending between chunks might fail because the difference in level between adjacent chunks is too high.  A great example of this is the Earth case.  Having a cloud layer for low levels and a non-cloud layer for higher levels requires level blending to be enabled to avoid visible chunk edges.  By disabling **levelByProjectedAreaElseDistance** for Earth, and enabling level blending, these edges should not be visible if all tiles have loaded.
  - **resetTileProviders** -- Resets all tile providers and clears the tile cache.  Resetting tile providers is useful if a change was done in a file and it needs to be reloaded. **Note however** that file paths used for tile providers are relative to the mod file where the RenderableGlobe was created.  This might cause a fail in re-opening tile datasets due to the fact that the runtime path has change since the initialisation.  In the future, we hope to never change the runtime path and only use absolute paths.  This will remove this issue.
  - **collectStats** -- **Boolean** value determining if stats should be collected and written to disc. The **ChunkedLodGlobe** uses a **StatsCollector** to gather values for **render time**, **number of chunk nodes**, **number of leaf nodes**, **number of rendered chunks**, **global time**. These values are saved as a CSV file in the path of the mod file for the renderable.
  - **limitLevelByAvailableData** -- **Boolean** value determining if chunk levels should be limited by the available data. If false, the chunks will split to higher levels even if there is no higher resolution tile data available.  To decrease render time, this should be enabled.
  - **modelSpaceRenderingCutoffLevel** -- **Integer** value setting the cutoff level between **model space rendering** and **camera space rendering**. This value should be between 10 and 16 to avoid artefacts such as precision jittering and flat tiles.
