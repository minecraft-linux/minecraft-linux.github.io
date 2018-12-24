Introduction (read first)
=========================

If you want to compile from sources make sure to install the basic prerequirements from below.

Basic prerequirements
---------------------
- **Ubuntu** - :code:`sudo apt-get install git cmake pkg-config`

What to build
-------------
- You will want to build MSA for Xbox Live support (for the client). Without it the game will not support signing in to Xbox Live.
- The game launcher to run the client.
- The Qt launcher UI if you want to easily download the .apk from Google Play and/or easily manage multiple Minecraft versions.
- The extract utility if you don't want to use the Qt launcher UI.

.. note:: **When building the server** you don't need to build MSA or the game launcher - only build the server and the Qt launcher or the extract utility.

Updating
--------
To update one of the components (so, :code:`msa`, :code:`mcpelauncher` or :code:`mcpelauncher-ui`), :code:`cd` to it's directory and run: :code:`git pull && git submodule update`. Then follow the same compile instructions as when doing a normal build, but skip the :code:`git clone` line. You'll still need to follow the install steps again afterwards.
