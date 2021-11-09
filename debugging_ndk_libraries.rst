Debugging ndk libraries
=======================

Use this with gdb to load debugging symbols of android libraries into you session https://stackoverflow.com/a/33087762.

You get the load address with https://github.com/minecraft-linux/mcpelauncher-linker/blob/5127987ca49c4aeca6d180f26a9a4ac5aa4501c2/src/linker.cpp#L21. Minecraft's load address is printed to the log as a hex number.

Development Utilities
~~~~~~~~~~~~~~~~~~~~~
Use readelf to list symbols of `libminecraftpe.so`

.. code:: bash

  readelf --wide -s libminecraftpe.so

Symbols with prefix :code:`java_` are callable java native interface functions.

Use :code:`dextojar` on :code:`classes.dex` of the android apk + https://java-decompiler.github.io/ on the jar file to get an idea how mojang implemented the java functions.

Glcore patch
~~~~~~~~~~~~
The Glcore patch is a patch to modifiy the android game to render on opengl 3.3 surfaces instead of opengl es 2, which is unavailable on macOS.

Due to absense of debugging symbols this patch is unavailable on 1.17+ and macOS builds use a fallback via an opengl es2 emulation layer called angle. The goal of section is to document how such a binary pattern has been created for 1.16.0.

To create such binary pattern to find the required function without the debugging symbols, you might be able to use this ida pro plugin https://github.com/ajkhoury/SigMaker-x64.
