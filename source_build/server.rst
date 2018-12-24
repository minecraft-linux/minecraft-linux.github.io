Compiling the server launcher
=============================

Prerequirements
---------------
- **Ubuntu** - :code:`sudo apt-get install git cmake pkg-config`
- **macOS** - :code:`brew install cmake`

Requirements
------------
- **Ubuntu** - you'll need to :code:`sudo dpkg --add-architecture i386`, then install the required packages: :code:`sudo apt-get install g++-multilib`
- **macOS** - none

Build instructions
------------------
.. code:: bash

   git clone --recursive https://github.com/minecraft-linux/mcpelauncher-manifest.git mcpelauncher && cd mcpelauncher
   mkdir -p build && cd build
   cmake -DBUILD_CLIENT=OFF ..
   make -j12

After compiling you should look at the :ref:`server` page.
