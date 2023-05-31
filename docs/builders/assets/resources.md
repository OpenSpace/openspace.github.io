---
title: Resources
layout: default

grand_parent: Builders
parent: Assets
nav_order: 1
---

# What are resources?

Resources are files that can be loaded as data into OpenSpace. A resource can for example consist of a movie, images, maps, positional data, etc. You can use two types of resources in OpenSpace:

1. **Local resources**: Files that you have stored locally on your computer. For example, a movie in your `Documents` folder.
1. **Synchronized resources**: Files that are stored on a server and downloaded when they are loaded into OpenSpace. For example, a map on our BigBang server.

# Local resources

To load a local resource into OpenSpace you need to specify a `path` to the file so that OpenSpace will know where it is located.

## What are paths?

Consider this file structure:
![A folder with a file](/assets/images/path_folder.png)

These are examples of paths to the file `myfile.txt`:

1. `C:/Users/yourname/Desktop/Documents/myfile.txt`
1. `./myfile.txt`

The first path is an **absolute path**. That means that the beginning of the path starts with one of your harddrives, usually `D:/` or `C:/`.

The second path is a **relative path**. A relative path means that the path is relative to the folder it is in. It starts with `./` to specify "the current folder".  In general, we recommend using relative paths where ever possible as it makes it less painful to later move asset files to another computer or share them with another user.

![A file referencing another file in the same folder](/assets/images/relative_path_folder.png)

For example, if you were to place a file in the folder `Documents` called `myResource.txt` you would be able to specify a relative path in the `myfile.txt` file with this relative path: `./myResource.txt`. **Important**: these files must be located in the same folder.

When loading a resource in an asset, you can either use an absolute path or a relative path.

## Using paths in assets

How can we write a path in an asset that loads this movie?

![An asset and a file in the same folder](/assets/images/asset_path.png)

### Absolute path

**Note**: paths in OpenSpace can only use forward slash `/`, never backward slash `\`.

For the absolute path, you can copy the text file explorer (see the cursor in the above image) and then add the filename. If your path contains backward slashes `\` you need to swap them out to forward slashes `/`. Then you need to surround the path with quotation marks.

Here is the absolute path for the movie above: `"C:/Users/yourname/Desktop/Documents/myVideo.mp4"`.

Here is an example of an asset where an absolute path is used for the `Video` property:

```
local layer = {
    Identifier = "ExampleVideoLocal",
    Video = "C:/Users/yourname/Desktop/Documents/myVideo.mp4",
    Name = "Example Video Local",
    Enabled = true,
    Type = "VideoTileLayer"
}

asset.onInitialize(function()
    openspace.globebrowsing.addLayer("Earth", "ColorLayers", layer)
end)

asset.onDeinitialize(function()
    openspace.globebrowsing.deleteLayer("Earth", "ColorLayers", layer)
end)

asset.export("layer", layer)

asset.meta = {
    Name = "Video Player Test",
    Version = "1.0",
    Description = "An example asset that shows how to include a video on Earth",
    Author = "OpenSpace Team",
    URL = "https://openspaceproject.com",
    License = "MIT"
}
```

The absolute path is set with `Video = "C:/Users/yourname/Desktop/Documents/myVideo.mp4"`.

## Relative path

**Note**: paths in OpenSpace can only use forward slash `/`, never backward slash `\`.

To use a relative path in an asset, the file you are referencing needs to be located in the same folder as the asset file. A relative path `./myFile.txt` is recognized by OpenSpace if it is written like this: `asset.localResource("./myFile.txt")`.

Here is the finished relative path for the movie above: `asset.localResource("./myVideo.mp4")`.

Here is an example of the video asset with a relative path used for the `Video` property:

```
local layer = {
    Identifier = "ExampleVideoLocal",
    Video = asset.localResource("./myVideo.mp4"),
    Name = "Example Video Local",
    Enabled = true,
    Type = "VideoTileLayer"
}

asset.onInitialize(function()
    openspace.globebrowsing.addLayer("Earth", "ColorLayers", layer)
end)

asset.onDeinitialize(function()
    openspace.globebrowsing.deleteLayer("Earth", "ColorLayers", layer)
end)

asset.export("layer", layer)

asset.meta = {
    Name = "Video Player Test",
    Version = "1.0",
    Description = "An example asset that shows how to include a video on Earth",
    Author = "OpenSpace Team",
    URL = "https://openspaceproject.com",
    License = "MIT"
}
```

The relative path is set with `Video = asset.localResource("./myVideo.mp4")`.

# Synchronized resources

There are two built-in mechanisms of resource synchronizations in OpenSpace: The `HttpSynchronization` and the `UrlSynchronization`. The `HttpSynchronization` is designed to fetch versioned data from the official OpenSpace server (data.openspaceproject.com), like this:

```
local path = asset.syncedResource({
    Type = "HttpSynchronization",
    Name = "Foo"
    Identifier = "foo",
    Version = 1
})
```

The UrlSynchronization can be used to fetch arbitrary data from the web.

```
local path = asset.syncedResource({
    Type = "UrlSynchronization",
    Name = "Bar",
    Identifier = "bar",
    Url = "http://example.com/data.zip",
    Override = true
})
```


The `Override` paramater can be used to force a new download even if the file has already previously been downloaded.
