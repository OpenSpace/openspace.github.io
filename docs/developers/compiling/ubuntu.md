---
title: Ubuntu
layout: default

grand_parent: Developers
parent: Compiling OpenSpace
nav_order: 3
nav_exclude: true
---

OpenSpace has been tested on Ubuntu versions 18.04 and 20.04.

# Developer Tools
Install the following tools:
 - Git 2.7+
 - GCC 9+
 - CMake 3.12+

## GCC
You can install gcc-9 using the following commands.  At the time of this writing, gcc-9 is not the default version in ubuntu 18.04 (but is default in 20.04), so this involves some additional steps.  The final commands configure ubuntu's "update-alternatives", which allows a user to select among multiple installations of gcc:
```
sudo apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade && sudo apt-get autoclean && sudo apt-get autoremove
```

reboot in case there are kernel changes

```
sudo apt-get install build-essential software-properties-common
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install gcc-9 g++-9
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 60 --slave /usr/bin/g++ g++ /usr/bin/g++-9
sudo update-alternatives --config gcc
```

If you don't want to install GCC 9 globally, you can overwrite the CMake options instead:
```
CMAKE_CXX_COMPILER:FILEPATH=/usr/bin/g++-9
CMAKE_C_COMPILER:FILEPATH=/usr/bin/gcc-9
```

If you do want to change the defaults: [here](https://stackoverflow.com/questions/7832892/how-to-change-the-default-gcc-compiler-in-ubuntu)

The CMake CXX flags variable should be set to:
`-DGLM_ENABLE_EXPERIMENTAL`

It is recommended to create a new CMake string variable `OPENGL_GL_PREFERENCE` and set its value to `GLVND`.

# Dependencies
Install the following libraries:


|    Package    |    Library    |
| ------------- | ------------- |
| [`glew-utils`](https://packages.ubuntu.com/bionic/glew-utils) | [OpenGL Extension Wrangler Library (GLEW)](http://glew.sourceforge.net/) |
|[`freeglut3-dev`](https://packages.ubuntu.com/bionic/freeglut3-dev)|[Free OpenGL Utility Toolkit (GLUT)](http://freeglut.sourceforge.net/)|
|[`libpng-dev`](https://packages.ubuntu.com/bionic/libpng-dev)|[PNG Library](http://www.libpng.org/pub/png/)|
|[`libxrandr-dev`](https://packages.ubuntu.com/bionic/libxrandr-dev)|[X Window System Protocol 11 (X11) Resize, Rotate and Reflection (XRandR) extension library (development headers)](https://salsa.debian.org/xorg-team/lib/libxrandr)|
|[`libxinerama-dev`](https://packages.ubuntu.com/bionic/libxinerama-dev)|[X Window System Protocol 11 (X11) Xinerama extension library (development headers)](https://salsa.debian.org/xorg-team/lib/libxinerama)|
|[`xorg-dev`](https://packages.ubuntu.com/bionic/xorg-dev)|[X.Org X Window System development libraries](http://www.x.org/)|
|[`libcurl4-openssl-dev`](https://packages.ubuntu.com/bionic/libcurl4-openssl-dev)|[Library for Client URL (cURL)(libcurl) - OpenSSL flavour](https://curl.haxx.se/)|
|[`libgdal-dev`](https://packages.ubuntu.com/bionic/libgdal-dev)|[Geospatial Data Abstraction Library (GDAL) - Development files](http://www.gdal.org/)|
|[`libxcursor-dev`](https://packages.ubuntu.com/bionic/libxcursor-dev)|[X cursor management library (development files)](https://www.x.org/)|
|[`git`](https://packages.ubuntu.com/bionic/git)|[git](https://git-scm.com/)|

  
```
sudo add-apt-repository -y ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install -y \
build-essential software-properties-common \
gcc-9 g++-9 cmake \
glew-utils freeglut3-dev libpng-dev \
libxrandr-dev libxinerama-dev xorg-dev libcurl4-openssl-dev libgdal-dev libxcursor-dev \
git
```

Note that a Qt5 installation is currently required (see general compile page). CMake will need help finding this install (for example, the required `Qt5_DIR` entry may be something like: /opt/Qt/5.15.0/gcc_64/lib/cmake/Qt5). In the future, this will be updated with the libQt5\*.so files which can be installed via `apt-get`.

# Compile OpenSpace

1) Checkout
1) Configure
1) Make

```
openSpaceHome="$HOME/source/OpenSpace"

git clone --recursive https://github.com/OpenSpace/OpenSpace "$openSpaceHome"

mkdir -p "$openSpaceHome/build"
cd "$openSpaceHome/build" || exit

cmake \
-DCMAKE_BUILD_TYPE:STRING="Release" \
-DCMAKE_CXX_COMPILER:FILEPATH=/usr/bin/g++-9 \
-DCMAKE_C_COMPILER:FILEPATH=/usr/bin/gcc-9 \
-DCMAKE_CXX_FLAGS:STRING="-DGLM_ENABLE_EXPERIMENTAL" \
-DOpenGL_GL_PREFERENCE:STRING=GLVND \
-DASSIMP_BUILD_MINIZIP=1 "$openSpaceHome"

make
```

### CMake step
This can be one of the following:
* `cmake ..` The simplest way if there are no CMake issues to resolve or build options to set.
* `ccmake ..` A curses pseudo-gui version of CMake (run `sudo apt install cmake-curses-gui` if not installed).
* `cmake-gui ..` A Qt GUI version of CMake.

With any of these methods, CMake is first configured, then (if no errors) the generate step creates the build files.

The Web GUI interface does not work with the linux version of OpenSpace. Use the F1 menu instead, which provides full functionality but has a different layout.

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
