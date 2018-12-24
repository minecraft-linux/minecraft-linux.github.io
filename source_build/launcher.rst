Compiling the game launcher
===========================

Prerequirements
---------------
- **Ubuntu** - you'll need to :code:`sudo dpkg --add-architecture i386`, then install the required packages:
  .. code::
   sudo apt-get install g++-multilib libpng-dev:i386 libx11-dev:i386 libxi-dev:i386 libcurl4-openssl-dev:i386 libudev-dev:i386 libevdev-dev:i386 libegl1-mesa-dev:i386 libasound2:i386

- **macOS** - :code:`brew install cmake libpng`

Build instructions
------------------
.. code:: bash

   git clone --recursive https://github.com/minecraft-linux/mcpelauncher-manifest.git mcpelauncher && cd mcpelauncher
   mkdir -p build && cd build
   cmake ..
   make -j12

**Important note:** Please note that you may need to replace `cmake ..` with `cmake -DMSA_DAEMON_PATH=/absolute/path/to/daemon/build/dir/msa-daemon ..` if you didn't install the MSA daemon (e.g. if you ran the previous command in /home/paul/, you'd have to use /home/paul/msa/build/msa-daemon as the path). Note the .. is preceded by a space and is not part of the path to the daemon.

Installation
------------

You can now optionally install the launcher system-wise. If you don't, you'll need to specify the path to the metalauncher later (and the resulting binary will only work on your system).

- **Generic instructions** - Run `sudo make install`. Note that this doesn't make use of your system package manager, and therefore if possible, it's generally not recommended if there are better alternatives available for your system.
- **Ubuntu** - You can create a .deb file and install it using the following commands:

  .. code:: bash

      cpack --config mcpelauncher-client/CPackConfig.cmake
      sudo dpkg -i  ./mcpelauncher-client-*-Linux.deb && sudo apt-get install -f

