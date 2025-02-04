# Debugging ndk libraries

Use this with gdb to load debugging symbols of android libraries into
your session <https://stackoverflow.com/a/33087762>.

You get the load address with
<https://github.com/minecraft-linux/mcpelauncher-linker/blob/5127987ca49c4aeca6d180f26a9a4ac5aa4501c2/src/linker.cpp#L21>.
Minecraft's load address is printed to the log as a hex number.

## codelldb

Works on linux, macOS and windows on both arm64 and intel

1. Install vscode
2. Install codelldb extension
3. Compile the launcher with `-DCMAKE_BUILD_TYPE=Debug`
4. Add the following property (only the python api seem to ignore that we load debug info of `.so` files into a macOS / windows process)
   ```json
   "preRunCommands": [
       "breakpoint set --name mcpelauncher_linker_notifylldb -C \"script lldb.debugger.GetSelectedTarget().SetModuleLoadAddress(lldb.debugger.GetSelectedTarget().AddModule(lldb.process.ReadCStringFromMemory(lldb.frame.FindVariable('filename').unsigned, 255, lldb.SBError()), '', ''), lldb.frame.FindVariable('offset').unsigned)\" --auto-continue true",
   ]
   ```
   mcpelauncher-linker exposes this function used as an automated breakpoint and calls it before calling the constructor of the game, the address is available in the cli output as well.
5. Enjoy having step debugging in mods compiled with debug information and better stack traces of the minecraft game

## Development Utilities

Use readelf to list symbols of `libminecraftpe.so`

``` bash
readelf --wide -s libminecraftpe.so
```

Symbols with prefix `java_` are callable java native interface
functions.

Use `dextojar` on `classes.dex` of the android apk +
<https://java-decompiler.github.io/> on the jar file to get an idea how
mojang implemented the java functions.

## Glcore patch

The Glcore patch is a patch to modifiy the android game to render on
opengl 3.3 surfaces instead of opengl es 2, which is unavailable on
macOS.

Due to absense of debugging symbols, is this patch unavailable on 1.17+
and macOS builds use a fallback via an opengl es2 emulation layer called
angle. The goal of this section is to document how such a binary pattern
has been created for 1.16.0.

To create such binary pattern to be able to find the required function
without the debugging symbols, you might be able to use this ida pro
plugin <https://github.com/ajkhoury/SigMaker-x64>.

For example here two patterns and the actual required function name of
the game
<https://github.com/minecraft-linux/mcpelauncher-client/blob/eb2465a1f59422b1cf11d14b9838eeb5d5c32237/src/gl_core_patch.cpp#L22>.
This symbol can be found via readelf on 1.16.201.
