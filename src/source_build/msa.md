# Compiling MSA (for Xbox Live)

**Not used for Xbox live in Minecraft 1.16.40+**

## Prerequisites

- **Ubuntu 18.04+** -
  `sudo apt-get install libssl-dev libcurl4-openssl-dev qtbase5-dev qtwebengine5-dev`
- **Ubuntu 16.04** - You must add a Qt 5.9+ repository first
  (`add-apt-repository ppa:beineri/opt-qt596-xenial && apt-get update`)
  from which you should install
  `apt-get install qt59base qt59webengine`; also install
  `apt-get install libssl-dev libcurl4-openssl-dev`
- **Fedora** (Up to date as of 2024-08-21) -
  `sudo dnf install openssl-devel libcurl-devel qt5-qtbase-devel qt5-qtwebengine-devel`
- **macOS** - `brew install cmake qt@5`

## Build instructions

``` bash
git clone --recursive https://github.com/minecraft-linux/msa-manifest.git msa && cd msa
mkdir -p build && cd build
cmake -DENABLE_MSA_QT_UI=ON ..
make -j$(getconf _NPROCESSORS_ONLN)
```

**macOS:** replace the `cmake` line with
`cmake -DCMAKE_PREFIX_PATH=$(brew --prefix qt@5) -DENABLE_MSA_QT_UI=ON ..`

## Installation

You can now optionally install the MSA daemon system-wise. If you don't,
you'll need to specify the path to MSA later (and the resulting binary
will only work on your system).

- **Generic instructions** - Run `sudo make install`. Note that this
  doesn't make use of your system package manager, and therefore if
  possible, it's generally not recommended if there are better
  alternatives available for your system.

**Important Note:** Before continuing to the next step, make sure to go
to the parent directory with `cd ../..` (make sure to return from the
build directory and then from the msa directory). This generally applies
to the following steps as well.
