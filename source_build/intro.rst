Introduction (read first)
=========================

If you want to compile from sources make sure to install the basic prerequirements from below.

Basic prerequirements
---------------------
- **Ubuntu** - :code:`sudo apt-get install git cmake pkg-config`
- **Fedora** - :code:`sudo dnf install git make cmake pkg-config`

What to build
-------------
- You will want to build MSA for Xbox Live support (for the client). Without it the game will not support signing in to Xbox Live.
- The game launcher to run the client.
- The Qt launcher UI if you want to easily download the .apk from Google Play and/or easily manage multiple Minecraft versions.
- The extract utility if you don't want to use the Qt launcher UI.

.. note:: **When building the server** you don't need to build MSA or the game launcher - only build the server and the Qt launcher or the extract utility.

Updating
--------
To update one of the components (so, :code:`msa`, :code:`mcpelauncher` or :code:`mcpelauncher-ui`), :code:`cd` to it's directory and run: :code:`git pull && git submodule update --recursive`. Then follow the same compile instructions as when doing a normal build, but skip the :code:`git clone` line. You'll still need to follow the install steps again afterwards.

.. _source_uninstall:

Uninstalling
------------
If you installed using :code:`make install` in order to uninstall do the following **as root** (escalate using :code:`sudo su`):

.. code:: bash

   rm /usr/local/bin/mcpelauncher-client
   rm /usr/local/bin/mcpelauncher-error
   rm /usr/local/bin/mcpelauncher-extract
   rm /usr/local/bin/mcpelauncher-ui-qt
   rm /usr/local/bin/mcpelauncher-webview
   rm /usr/local/bin/msa-daemon
   rm /usr/local/bin/msa-ui-qt
   rm /usr/local/share/applications/mcpelauncher-ui-qt.desktop
   rm -r /usr/local/share/mcpelauncher/

Some of the commands may return errors - that's fine as some modules simply could have been not installed.
