.. _source_build_launcher:

Compiling the game launcher
===========================

Prerequirements
---------------
- **Ubuntu** (Up to date as of 2023-04-09) - you'll need to install the required packages: :code:`sudo apt-get install --no-install-recommends g++ clang cmake make git ca-certificates libssl-dev libpng-dev libx11-dev libxi-dev libcurl4-openssl-dev libudev-dev libevdev-dev libegl1-mesa-dev libssl-dev libasound2 qtbase5-dev qtwebengine5-dev qtdeclarative5-dev libqt5svg5-dev qml-module-qtquick2 qml-module-qtquick-layouts qml-module-qtquick-controls qml-module-qtquick-controls2 qml-module-qtquick-window2 qml-module-qtquick-dialogs qml-module-qt-labs-settings qml-module-qt-labs-folderlistmodel qml-module-qtwebengine libstdc++-12-dev`
- **Fedora** (Needs verification) - you'll need to install the required packages: :code:`sudo dnf install gcc-c++ clang cmake make git ca-certificates libstdc++ glibc-devel libpng-devel zlib-devel libX11-devel libXi-devel libcurl-devel systemd-devel libevdev-devel mesa-libEGL-devel alsa-lib pulseaudio-libs mesa-dri-drivers systemd-devel libXtst-devel openssl-devel qt5-qtbase-devel qt5-qtwebengine-devel qt5-qtdeclarative-devel qt5-qtsvg-devel qt5-qtquickcontrols qt5-qtquickcontrols2`
- **macOS** - :code:`brew install cmake libpng openssl@1.1 qt@5`

Build instructions
------------------
.. code:: bash

   git clone --recursive https://github.com/minecraft-linux/mcpelauncher-manifest.git mcpelauncher && cd mcpelauncher
   mkdir -p build && cd build
   CC=clang CXX=clang++ cmake .. -Wno-dev -DCMAKE_BUILD_TYPE=Release -DJNI_USE_JNIVM=ON 
   make -j$(getconf _NPROCESSORS_ONLN)
   
**macOS:** Add the following options to the cmake command: :code:`-DOPENSSL_ROOT_DIR=$(brew --prefix openssl@1.1) -DCMAKE_PREFIX_PATH=$(brew --prefix qt@5)`.

**Important note:** Please note that you may need to replace `cmake ..` with `cmake -DMSA_DAEMON_PATH=/absolute/path/to/daemon/build/dir/msa-daemon ..` if you didn't install the MSA daemon (e.g. if you ran the previous command in /home/paul/, you'd have to use /home/paul/msa/build/msa-daemon as the path). Note the .. is preceded by a space and is not part of the path to the daemon.

Installation
------------

You can now optionally install the launcher system-wise. If you don't, you'll need to specify the path to the metalauncher later (and the resulting binary will only work on your system).

- **Generic instructions** - Run `sudo make install`. Note that this doesn't make use of your system package manager, and therefore if possible, it's generally not recommended if there are better alternatives available for your system.
- **Ubuntu** (Outdated as of 2021-07-27) - You can create a .deb file and install it using the following commands:

  .. code:: bash

      cpack --config mcpelauncher-client/CPackConfig.cmake
      sudo dpkg -i  ./mcpelauncher-client-*-Linux.deb && sudo apt-get install -f
