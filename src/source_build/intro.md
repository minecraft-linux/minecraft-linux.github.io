# Introduction (read first)

If you want to compile from sources make sure to install the basic
prerequirements from below.

## Basic Prerequisites

- **Ubuntu** - `sudo apt-get install git cmake pkg-config`
- **Fedora** - `sudo dnf install git make cmake pkg-config`

## What to build

- You will want to build MSA for Xbox Live support (for the client).
  Without it the game will not support signing in to Xbox Live.
- The game launcher to run the client.
- The Qt launcher UI if you want to easily download the .apk from Google
  Play and/or easily manage multiple Minecraft versions.
- The extract utility if you don't want to use the Qt launcher UI.

## Updating

To update one of the components (so, `msa`, `mcpelauncher` or
`mcpelauncher-ui`), `cd` to it's directory and run:
`git pull && git submodule update --recursive`. Then follow the same
compile instructions as when doing a normal build, but skip the
`git clone` line. You'll still need to follow the install steps again
afterwards.

## Uninstalling

If you installed using `make install` in order to uninstall do the
following **as root** (escalate using `sudo su`):

``` bash
   rm /usr/local/bin/mcpelauncher-client
   rm /usr/local/bin/mcpelauncher-client
   rm -r /usr/local/share/mcpelauncher
   rm /usr/local/bin/mcpelauncher-error
   rm /usr/local/bin/mcpelauncher-extract
   rm /usr/local/bin/mcpelauncher-ui-qt
   rm /usr/local/bin/mcpelauncher-ui-qt
   rm /usr/local/bin/mcpelauncher-webview
   rm /usr/local/bin/msa-daemon
   rm /usr/local/bin/msa-ui-qt
   rm /usr/local/share/applications/mcpelauncher-ui-qt.desktop
   rm /usr/local/share/applications/mcpelauncher-ui-qt.desktop
   rm /usr/local/share/pixmaps/mcpelauncher-ui-qt.png
   rm -r /usr/local/share/mcpelauncher/
```

Some of the commands may return errors - that's fine as some modules
simply could have been not installed.
