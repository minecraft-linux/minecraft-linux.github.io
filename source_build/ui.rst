Compiling the Qt UI
===================

Prerequirements
---------------
- **Ubuntu 18.04+** - :code:`sudo apt-get install libssl-dev libcurl4-openssl-dev libuv1-dev libzip-dev libprotobuf-dev protobuf-compiler qtbase5-dev qtwebengine5-dev qtdeclarative5-dev libqt5svg5-dev qml-module-qtquick2 qml-module-qtquick-layouts qml-module-qtquick-controls qml-module-qtquick-controls2 qml-module-qtquick-window2 qml-module-qtquick-dialogs qml-module-qt-labs-settings qml-module-qt-labs-folderlistmodel`
- **Ubuntu 16.04** - You must add a Qt 5.9+ repository first (:code:`add-apt-repository ppa:beineri/opt-qt596-xenial && apt-get update`, you probably have done this when compiling MSA already) from which you should install :code:`apt-get install qt59base qt59declarative qt59quickcontrols qt59quickcontrols2 qt59webengine`; also install :code:`apt-get install libssl-dev libcurl4-openssl-dev libuv1-dev libzip-dev libprotobuf-dev protobuf-compiler`
- **Fedora** (Up to date as of 2024-08-21)- :code:`sudo dnf install libuv-devel libzip-devel protobuf-devel protobuf-compiler qt5-qtbase-devel qt5-qtwebengine-devel qt5-qtdeclarative-devel qt5-qtsvg-devel qt5-qtquickcontrols qt5-qtquickcontrols2 libcurl-devel libXrandr-devel libXinerama-devel libXcursor-devel libXi-devel`
- **macOS** - :code:`brew install cmake qt@5 libzip libuv protobuf`
- :ref:`the game launcher <source_build_launcher>`

Build instructions
------------------
.. code:: bash

   git clone --recursive https://github.com/minecraft-linux/mcpelauncher-ui-manifest.git mcpelauncher-ui
   cd mcpelauncher-ui && mkdir -p build && cd build
   cmake ..
   make -j$(getconf _NPROCESSORS_ONLN)

**macOS:** replace the :code:`cmake` line with :code:`cmake -DCMAKE_PREFIX_PATH=$(brew --prefix qt@5) ..`

If you haven't installed the launcher system-wide, please replace :code:`cmake ..` with :code:`cmake -DGAME_LAUNCHER_PATH=/absolute/path/to/mcpelauncher/build/dir/mcpelauncher-client ..` (if you compiled the mcpelauncher-manifest in /home/paul, then you'd have to use :code:`cmake -DGAME_LAUNCHER_PATH=/home/paul/mcpelauncher-manifest/build/mcpelauncher-client ..` as the command).

Installation
------------
You can now optionally install the launcher system-wise.

- **Generic instructions** - Run `sudo make install`. Note that this doesn't make use of your system package manager, and therefore if possible, it's generally not recommended if there are better alternatives available for your system.
- **Ubuntu** - You can create a .deb file and install it using the following commands:

  .. code:: bash

      cpack --config mcpelauncher-ui-qt/CPackConfig.cmake
      sudo dpkg -i  ./mcpelauncher-ui-qt-*-Linux.deb && sudo apt-get install -f

