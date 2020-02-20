---
title: ChunkRendering
layout: default

grand_parent: Developers
parent: Globebrowsing
nav_order: 2
---

# Chunk Rendering
The base of chunk rendering takes place in **rendering/chunkrenderer.cpp**.  The two functions `renderChunkGlobally` and `renderChunkLocally` are used for model space rendering and camera space rendering respectively.

## Shader Uniforms
Since the shader compiler usually removes all unused code it is important not to upload any uniforms to the shader that will not be in use.  This will result in error messages.  Therefore we use if-statements such as `if (_layerManager->hasAnyBlendingLayersEnabled())` to determine whether or not to upload certain uniforms.  Some uniforms are specific for either one of the rendering methods, and some are common for both of them.  Since the fragment pipeline is identical for camera space and model space rendering, all these uniforms are the same.

## Shader Preprocessing
We use the ghoul shader preprocessor to opt out any unused layers or settings in the pipeline.  This causes some awkward shader syntax which is visible mainly in **shaders/texturetilemapping.hglsl**.  One example is the function `getSample...` which gets the sample for all layers of all types.  This is a "template" function in the way that the preprocessor will resolve its contents for all layer groups and for all active layers within that loop.  Not all layer types are tile layers, therefore we check the layer type in this function with preprocessor statements to determine whether or not to sample from a layer.  **ColorLayers** for example, will just set the color according to the color uniform while all tile layers will call the `getTexVal` function.

### Preprocessing Data
The `LayerShaderManager` takes care of preprocessor values that are added to the shaders before they are resolved.  As you can see in the function `LayerShaderManager::LayerShaderPreprocessingData::get`, Values can be added such as `pairs.emplace_back("useAccurateNormals", std::to_string(generalProps.useAccurateNormals));`.  These values can then be accessible in the shaders like so: `#{useAccurateNormals}`.

The preprocessing data also contains all info about all the active layers.  `lastLayerIdx` is defined as `number of active layers - 1` for all layer groups.  Then each layer has a `layerType`, a `blendMode`, and a `layerAdjustmentType`.  These are vectors containing the information for each layer given its index in the vector.

Every time a setting that affects the preprocessing data of a given globe is updated, the shaders need to be recompiled.  The function used to recompile is propagated down to all layers as `Layer::onChange` in **rendering/layer/layer.cpp**.

If a setting is added, it should be considered whether it is suitable as a uniform or as a preprocessing statement.
