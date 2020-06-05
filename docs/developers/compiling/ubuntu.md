---
title: Ubuntu
layout: default

grand_parent: Developers
parent: Compiling OpenSpace
nav_order: 3
---

OpenSpace has been tested on version 18.04 of ubuntu.
## Please note that as of May 2020, the current version of OpenSpace runs but is not rendering correctly on Ubuntu (see github issues for more information).

# Developer Tools
Install the following tools:
 - Git 2.7+
 - GCC 8+
 - CMake 3.12+

## GCC
You can install gcc-8 using the following commands.  At the time of this writing, gcc-8 is not the default version in ubuntu, so this involves some additional steps.  The final commands configure ubuntu's "update-alternatives", which allows a user to select among multiple installations of gcc: 
```
sudo apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade && sudo apt-get autoclean && sudo apt-get autoremove
```

reboot in case there are kernel changes

```
sudo apt-get install build-essential software-properties-common
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install gcc-8 g++-8
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 60 --slave /usr/bin/g++ g++ /usr/bin/g++-8
sudo update-alternatives --config gcc
```

If you don't want to install GCC 8 globally (e.g. leave gcc 7 as the default for ubuntu), you can overwrite the CMake options instead:
```
CMAKE_CXX_COMPILER:FILEPATH=/usr/bin/g++-8
CMAKE_C_COMPILER:FILEPATH=/usr/bin/gcc-8
```

If you do want to change the defaults: [here](https://stackoverflow.com/questions/7832892/how-to-change-the-default-gcc-compiler-in-ubuntu)

The CMake CXX flags variable should be set to:
`CMAKE_CXX_FLAGS:STRING=-std=gnu++17 -DGLM_ENABLE_EXPERIMENTAL`

It is recommended to create a new CMake string variable `OPENGL_GL_PREFERENCE` and set its value to `GLVND`.

# Dependencies
Install the following libraries:


|    Package    |    Library    |
| ------------- | ------------- |
| [`glew-utils`](https://packages.ubuntu.com/bionic/glew-utils) | [OpenGL Extension Wrangler Library (GLEW)](http://glew.sourceforge.net/) |
|[`freeglut3-dev`](https://packages.ubuntu.com/bionic/freeglut3-dev)|[Free OpenGL Utility Toolkit (GLUT)](http://freeglut.sourceforge.net/)|
|[`libsoil1`](https://packages.ubuntu.com/bionic/libsoil1)*|[Simple OpenGL Image Library (SOIL)](http://www.lonesock.net/soil.html)|
|[`libxrandr-dev`](https://packages.ubuntu.com/bionic/libxrandr-dev)|[X Window System Protocol 11 (X11) Resize, Rotate and Reflection (XRandR) extension library (development headers)](https://salsa.debian.org/xorg-team/lib/libxrandr)|
|[`libxinerama-dev`](https://packages.ubuntu.com/bionic/libxinerama-dev)|[X Window System Protocol 11 (X11) Xinerama extension library (development headers)](https://salsa.debian.org/xorg-team/lib/libxinerama)|
|[`xorg-dev`](https://packages.ubuntu.com/bionic/xorg-dev)|[X.Org X Window System development libraries](http://www.x.org/)|
|[`libcurl4-openssl-dev`](https://packages.ubuntu.com/bionic/libcurl4-openssl-dev)|[Library for Client URL (cURL)(libcurl) - OpenSSL flavour](https://curl.haxx.se/)|
|[`libgdal-dev`](https://packages.ubuntu.com/bionic/libgdal-dev)|[Geospatial Data Abstraction Library (GDAL) - Development files](http://www.gdal.org/)|
|[`libxcursor-dev`](https://packages.ubuntu.com/bionic/libxcursor-dev)|[X cursor management library (development files)](https://www.x.org/)|
|[`git`](https://packages.ubuntu.com/bionic/git)|[git](https://git-scm.com/)|


\* The recommended image library for Linux.  While [FreeImage](https://freeimage.sourceforge.io/) seems to work well with OpenSpace on other platforms, problems have been encountered while using this on Linux
  
```
sudo add-apt-repository -y ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install -y \
build-essential software-properties-common \
gcc-8 g++-8 cmake \
glew-utils freeglut3-dev libsoil1 \
libxrandr-dev libxinerama-dev xorg-dev libcurl4-openssl-dev libgdal-dev libxcursor-dev \
git
```

# Compile OpenSpace

1) Checkout
1) Configure
1) Make

```
openSpaceHome="$HOME/source/OpenSpace"

git clone --recursive --branch linux https://github.com/OpenSpace/OpenSpace "$openSpaceHome"

mkdir -p "$openSpaceHome/build"
cd "$openSpaceHome/build" || exit

cmake \
-DCMAKE_CXX_COMPILER:FILEPATH=/usr/bin/g++-8 \
-DCMAKE_C_COMPILER:FILEPATH=/usr/bin/gcc-8 \
-DCMAKE_CXX_FLAGS:STRING="-std=gnu++17 -DGLM_ENABLE_EXPERIMENTAL" \
-DOpenGL_GL_PREFERENCE:STRING=GLVND "$openSpaceHome"

make
```

### CMake step
This can be one of the following:
* `cmake ..` The simplest way if there are no CMake issues to resolve or build options to set.
* `ccmake ..` A curses pseudo-gui version of CMake (run `sudo apt install cmake-curses-gui` if not installed).
* `cmake-gui ..` A Qt GUI version of CMake.

With any of these methods, CMake is first configured, then (if no errors) the generate step creates the build files.

# Run OpenSpace

Execute:

```
"$openSpaceHome"/bin/OpenSpace
```

# Troubleshooting
Make sure that you are using the correct version of gcc/g++  
 - Double check `CMAKE_CXX_COMPILER` and `/usr/bin/c++ --version` to be sure.  It should be at least 8.0

Error: libstdc++.so.6: could not read symbols: Missing DSO from command line  
 - Try using g++ instead of gcc.

Error: GLSL 3.00 is not supported.  Supported versions are: 1.10, 1.20, 1.30, 1.00 ES, and 3.00 ES  
 - Enter the following line in the terminal before running, or add this to `~/.bashrc` or `~/.profile`:
 `export MESA_GL_VERSION_OVERRIDE=4.3`
 
It may be necessary to install boost if trying to build some of the older branches.
