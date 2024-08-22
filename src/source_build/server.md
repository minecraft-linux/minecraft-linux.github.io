# DEPRECATED server launcher

## Prerequisites

-   **Ubuntu** - `sudo apt-get install git cmake pkg-config`
-   **Fedora** -
    `sudo dnf install git make cmake pkg-config gcc-c++ libstdc++.i686 glibc-devel.i686`
-   **macOS** - `brew install cmake`

## Requirements

-   **Ubuntu** - you\'ll need to `sudo dpkg --add-architecture i386`,
    then install the required packages:
    `sudo apt-get install g++-multilib`
-   **macOS** - none

## Build instructions

``` bash
git clone --recursive https://github.com/minecraft-linux/mcpelauncher-manifest.git -b master mcpelauncher && cd mcpelauncher
mkdir -p build && cd build
cmake -DBUILD_CLIENT=OFF ..
make -j$(getconf _NPROCESSORS_ONLN)
```
