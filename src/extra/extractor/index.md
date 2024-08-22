# Extract utility

The extract utility is a simple utility for extracting the game from an
.apk file.

The utility is not provided as a binary, because it is stand-alone and
really straightforward to compile.

## Usage

`mcpelauncher-extract <source .apk> <destination dir>`

The client binary can use any directory as the game directory, but
generally the preference is to use
`~/.local/share/mcpelauncher/versions/1.2.3.4` as the directory for a
given version, as this allows you to easily multiversion the game. This
means, that if you have a file called `mcpe.apk` in the current working
directory and it is of the 1.5.3.0 version of Minecraft and would simply
like to extract it, you can do it as follows: \|
`mkdir -p ~/.local/share/mcpelauncher/versions/ && mcpelauncher extract mcpe.apk ~/.local/share/mcpelauncher/versions/1.5.3.0`

To start a given version of Minecraft you can then run the
`mcpelauncher-client` with the `-dg` argument, eg.
`mcpelauncher-client -dg ~/.local/share/mcpelauncher/versions/1.5.3.0`

## Build instructions

### Prerequirements

- Ubuntu - `sudo apt-get install cmake libzip-dev`
- macOS - `brew install cmake libzip`

### Compiling

``` bash
git clone https://github.com/minecraft-linux/mcpelauncher-extract.git -b ng
cd mcpelauncher-extract && mkdir -p build && cd build
cmake ..
make -j12
```
