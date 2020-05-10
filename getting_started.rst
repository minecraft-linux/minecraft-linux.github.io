Getting started
===============

A note for new users
--------------------

**This repository is currently not compatible with the latest versions of Minecraft: Bedrock Edition.**
However, there is an active fork of this repo that does run the latest versions. Both repositories are also undergoing a rewrite to support the new 64Bit versions of Bedrock Edition (Hooray Catalina users!). You can find links For Linux and Mac OS builds below.

Linux - https://github.com/ChristopherHX/linux-packaging-scripts/releases

MacOS - https://github.com/ChristopherHX/mcpelauncher-manifest/releases



MacOS
-----
A prebuilt **macOS binary** is `available here <https://mrarm.io/r/mcpelauncher-osx>`__.

If you want to compile from sources on macOS `go here <https://github.com/minecraft-linux/osx-packaging-scripts/wiki>`__.

Linux Mint
----------
Please note that Mint 19 **DOES NOT** equal Ubuntu 19.04. Use the :code:`Ubuntu 18.04` instructions for Mint 19.

Ubuntu 19.04
------------
.. code:: bash

   sudo dpkg --add-architecture i386
   wget -O - https://mcpelauncher.mrarm.io/apt/conf/public.gpg.key | sudo apt-key add -
   sudo add-apt-repository 'deb http://mcpelauncher.mrarm.io/apt/ubuntu/ disco main'
   sudo apt-get install msa-daemon msa-ui-qt mcpelauncher-client mcpelauncher-ui-qt

You will need to install 32 bit graphics drivers - for integrated graphics and most AMD GPUs :code:`libegl1-mesa-dev:i386` will work.

Ubuntu 18.04 and 18.10
----------------------
.. code:: bash

   sudo dpkg --add-architecture i386
   wget -O - https://mcpelauncher.mrarm.io/apt/conf/public.gpg.key | sudo apt-key add -
   sudo add-apt-repository 'deb http://mcpelauncher.mrarm.io/apt/ubuntu/ bionic main'
   sudo apt install msa-daemon msa-ui-qt mcpelauncher-client mcpelauncher-ui-qt

You will need to install 32 bit graphics drivers - for integrated graphics and most AMD GPUs :code:`libegl1-mesa:i386 libegl1-mesa-dev:i386` will work.

If you want to compile from sources on Ubuntu 18.04 or 18.10 `go here <https://github.com/minecraft-linux/linux-packaging-scripts/wiki#ubuntu-1804>`__.

Ubuntu 16.04
------------
.. code:: bash

   sudo dpkg --add-architecture i386
   sudo add-apt-repository -y ppa:beineri/opt-qt596-xenial
   wget -O - https://mcpelauncher.mrarm.io/apt/conf/public.gpg.key | sudo apt-key add -
   sudo add-apt-repository 'deb http://mcpelauncher.mrarm.io/apt/ubuntu/ xenial main'
   sudo apt update
   sudo apt install msa-daemon msa-ui-qt mcpelauncher-client mcpelauncher-ui-qt
   # To launch do: . /opt/qt59/bin/qt59-env.sh && mcpelauncher-ui-qt

You will need to install 32 bit graphics drivers - for integrated graphics and most AMD GPUs :code:`libegl1-mesa:i386 libegl1-mesa-drivers:i386` will work.

If you want to compile from sources on Ubuntu 16.04 `go here <https://github.com/minecraft-linux/linux-packaging-scripts/wiki#ubuntu-1604>`__.

Arch
----
There are **Arch AUR packages** available: :code:`mcpelauncher-msa-git mcpelauncher-msa-ui-qt-git` for Xbox Live support (you need to install both), :code:`mcpelauncher-linux-git` for the actual launcher and :code:`mcpelauncher-ui-git` for the metalauncher (recommended). You will need to enable the `multilib repository <https://wiki.archlinux.org/index.php/Official_repositories#multilib>`__. For audio support, you need to install :code:`lib32-libpulse` and :code:`lib32-alsa-plugins`.

So, summing it up you should install: :code:`mcpelauncher-msa-git mcpelauncher-msa-ui-qt-git mcpelauncher-linux-git mcpelauncher-ui-git lib32-libpulse lib32-alsa-plugins`

AppImage
--------

A prebuilt **AppImage binary** is `available here <https://mcpelauncher.mrarm.io/appimage/Minecraft_Bedrock_Launcher.AppImage>`__. After downloading simply open terminal, :code:`chmod +x Minecraft_Bedrock_Launcher.AppImage` and run it.

This is generally the preferred way if your OS is not one of the ones listed above.

Source build
------------
If there are no packages available for your distribution, check out the |Source build guide|_.

You can also use the `Linux build script <https://github.com/minecraft-linux/linux-packaging-scripts/wiki>`__.

.. |Source build guide| replace:: **Source build guide**
.. _Source build guide: https://github.com/minecraft-linux/mcpelauncher-manifest/wiki/Compiling-from-sources

Getting help
------------
We have a Discord chatroom, which you can join using the following link: https://discord.gg/TaUNBXr
