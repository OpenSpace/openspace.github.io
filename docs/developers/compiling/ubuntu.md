---
title: Ubuntu
layout: default

grand_parent: Developers
parent: Compiling OpenSpace
nav_order: 3
---

OpenSpace has been tested on version 18.04 of ubuntu.

# Developer Tools
Install the following tools:
 - Git 2.7+
 - GCC 8+
 - CMake 3.12+

## GCC
You can install gcc-8 using the following commands.  At the time of this writing, gcc-8 is not the default version in ubuntu, so this involves some additional steps.  The final commands configure ubuntu's "update-alternatives", which allows a user to select among multiple installations of gcc: 
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
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
CMAKE_CXX_FLAGS:STRING=-std=gnu++17
CMAKE_C_COMPILER:FILEPATH=/usr/bin/gcc-8
```

If you do want to change the defaults: [here](https://stackoverflow.com/questions/7832892/how-to-change-the-default-gcc-compiler-in-ubuntu)

# Libraries
Install the following libraries:
- GLEW (`sudo apt-get install glew-utils`)
- freeglut (`sudo apt-get install freeglut3-dev`)
- SOIL is the recommended image library for Linux (`sudo apt-get install libsoil1`).  While FreeImage seems to work well with OpenSpace on other platforms, problems have been encountered while using this on Linux
- Install other libraries using `sudo apt-get install <libname>`:
  * `libxrandr-dev`
  * `libxinerama-dev`
  * `xorg-dev`
  * `libcurl4-ssl-dev` (use `libcurl4-openssl-dev` if Ubuntu)
  * `libboost-dev`
  * `libboost-chrono-dev`
  * `libboost-system-dev`
  * `libboost-date-time-dev`
  * `libboost-thread-dev`
  * `libgdal-dev`
  * `libxcursor-dev`

# OpenSpace
Obtain the source code (develop branch in this case)
* `git clone --recursive https://github.com/OpenSpace/OpenSpace`
* `cd OpenSpace`

# Set up the build and run CMake
Basic steps:
* `mkdir build`
* `cd build`
* `cmake ..`
* `make`

If the CMake process does not complete because of issues that need to be resolved, or if build options need to be changed, then use the curses version of CMake (run `sudo apt install cmake-curses-gui` if not installed):
* `cd build`
* `ccmake ..`
* Select (c)onfigure and resolve any issues that are listed, or change CMake variables for the build.
* Select (g)enerate Makefile
* `make`

# Troubleshooting
Make sure that you are using the correct version of gcc/g++  
 - Double check `CMAKE_CXX_COMPILER` and `/usr/bin/c++ --version` to be sure.  It should be at least 8.0

Error: libstdc++.so.6: could not read symbols: Missing DSO from command line  
 - Try using g++ instead of gcc.

Error: GLSL 3.00 is not supported.  Supported versions are: 1.10, 1.20, 1.30, 1.00 ES, and 3.00 ES  
 - Enter the following line in the terminal before running, or add this to `~/.bashrc` or `~/.profile`:
 `export MESA_GL_VERSION_OVERRIDE=4.3`
