Getting started
===============

This launcher has been rewritten in 2020 to use mainly a fake Java Native Interface to communicate with Minecraft: Bedrock Edition. Additionally shortly after the release of the first 64bit versions on the Google Play Store, this previously 32bit only Launcher has been ported to arm64 and x86_64.

AppImage
--------
Prebuilt **AppImage binary's** `for linux x86_64, x86, armv7 hardfloat and armv8 are currently available here <https://github.com/ChristopherHX/linux-packaging-scripts/releases/latest>`__.
After downloading simply open terminal, :code:`chmod +x Minecraft_Bedrock_Launcher-x86_64.0.0.661.AppImage` and run it.
With some Filemanagers you should be able to run it with double click, similar to running a :code:`*.exe` file on Windows.
Otherwise run it from a Terminal :code:`./Minecraft_Bedrock_Launcher-x86_64.0.0.661.AppImage`

If it's your first time you have installed an AppImage and you want an Icon in your startmenu

- install `AppImageLauncher <https://github.com/TheAssassin/AppImageLauncher>`__
- run the AppImage like before
- AppImageLauncher will ask you to integrate it, press yes
- You can now start and update the Launcher directly from your startmenu

Flatpak
-------
You can also install mcpelauncher on Linux via `Flathub <https://flathub.org/apps/details/io.mrarm.mcpelauncher>`__.
To install it, first `setup Flatpak <https://flatpak.org/setup/>`__ then run

Install / Update System Wide
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code:: bash

   sudo flatpak install flathub io.mrarm.mcpelauncher

To update the launcher if already installed you can run this command

.. code:: bash

   sudo flatpak update
   
Install / Update User
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code:: bash

   flatpak install --user flathub io.mrarm.mcpelauncher

To update the launcher if already installed you can run this command

.. code:: bash

   flatpak update
   
Run
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If it's your first time you have installed a Flatpak please logout from your Computer and sign back in to be able to find the Launcher inside your startmenu.

To run it from a Teriminal, run

.. code:: bash

   flatpak run io.mrarm.mcpelauncher

If it doesn't start you can enable debug logging like this

.. code:: bash

   flatpak run io.mrarm.mcpelauncher -v

Debian, Ubuntu and Fedora repo
------------------------------

`How to add the apt or rpm repository <https://github.com/minecraft-linux/pkg>`__.

Once added you can install the :code:`mcpelauncher-manifest`, :code:`mcpelauncher-ui-manifest` and :code:`msa-manifest` packages to install the launcher system wide.



Debian / Ubuntu
^^^^^^^^^^^^^^^

.. code:: bash

   sudo apt update
   sudo apt install mcpelauncher-manifest mcpelauncher-ui-manifest msa-manifest

Fedora
^^^^^^

.. code:: bash

   sudo dnf install mcpelauncher-manifest mcpelauncher-ui-manifest msa-manifest

Run
^^^

You can find it in the startmenu or run the following command

.. code:: bash

   mcpelauncher-ui-qt

If it doesn't start you can enable debug logging like this

.. code:: bash

   mcpelauncher-ui-qt -v

macOS
-----
Prebuilt **macOS binary's** are `currently available here <https://github.com/ChristopherHX/osx-packaging-scripts/releases/latest>`__.
Always copy the App to a writeable location otherwise the updater won't work.

If you want to compile from sources on macOS `go here (Outdated as of 2021-07-27)
<https://github.com/minecraft-linux/osx-packaging-scripts/wiki>`__.

Source build
------------
If there are no packages available for your distribution, check out the :ref:`Source Build` guide.

You can also use the `Linux build script (Outdated as of 2021-07-27) <https://github.com/minecraft-linux/linux-packaging-scripts/wiki>`__.
