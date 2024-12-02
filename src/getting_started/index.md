# Getting started

The Unofficial *NIX Lancher for Minecraft is an **unofficial** launcher for the Android version
the Minecraft Bedrock Edition. It uses uses fake JNI (Java Native
Interface) to communicate with Minecraft. Unofficial *NIX Lancher for Minecraft supports x86,
x86_64, armhf, and arm64 versions of Minecraft on both Linux and MacOS

# Installation

## Linux

The Unofficial *NIX Lancher for Minecraft can be installed in many ways, however the primary
method of installation is with the Appimage

### AppImage

Prebuilt linux **AppImages** are available on
[AppImage Builder on Github](https://github.com/minecraft-linux/appimage-builder/releases/latest)
After downloading simply open terminal,
`chmod +x Minecraft_Bedrock_Launcher-*.AppImage` and run
it. With some Filemanagers you should be able to run it with double
click, similar to running a `*.exe` file on Windows. Otherwise run it
from a Terminal `./Minecraft_Bedrock_Launcher-*.AppImage `

#### Updating

To Upgrade, simply remove the old appimage and download the new version
using the above steps

#### Startmenu Integration

If it's your first time you have installed an AppImage and you want an
Icon in your startmenu

- install
  [AppImageLauncher](https://github.com/TheAssassin/AppImageLauncher)
- run the AppImage like before
- AppImageLauncher will ask you to integrate it, press yes
- You can now start and update the Launcher directly from your startmenu

### Flatpak

You can also install mcpelauncher on Linux via
[Flathub](https://flathub.org/apps/details/io.mrarm.mcpelauncher). To
install it, first [setup Flatpak](https://flatpak.org/setup/) then run

#### Install / Update System Wide

``` bash
sudo flatpak install flathub io.mrarm.mcpelauncher
```

To update the launcher if already installed you can run this command

``` bash
sudo flatpak update
```

#### Install / Update User

``` bash
flatpak install --user flathub io.mrarm.mcpelauncher
```

To update the launcher if already installed you can run this command

``` bash
flatpak update
```

#### Run

If it's your first time you have installed a Flatpak please logout from
your Computer and sign back in to be able to find the Launcher inside
your startmenu.

To run it from a Terminal, run

``` bash
flatpak run io.mrarm.mcpelauncher
```

If it doesn't start you can enable debug logging like this

``` bash
flatpak run io.mrarm.mcpelauncher -v
```

### Debian, Ubuntu and Fedora repo

[How to add the apt or rpm
repository](https://github.com/minecraft-linux/pkg).

Once added you can install the `mcpelauncher-manifest`,
`mcpelauncher-ui-manifest` and `msa-manifest` packages to install the
launcher system wide.

#### Debian / Ubuntu

``` bash
sudo apt update
sudo apt install mcpelauncher-manifest mcpelauncher-ui-manifest msa-manifest
```

#### Fedora

``` bash
sudo dnf install mcpelauncher-manifest mcpelauncher-ui-manifest msa-manifest
```

### Arch User Repository (AUR) Package

**Unofficial** packages for Arch Linux users can be installed on the AUR, both [client](https://aur.archlinux.org/packages/mcpelauncher-linux) and [Qt launcher](https://aur.archlinux.org/packages/mcpelauncher-ui). You can install using an appropriate AUR helper such as yay.

``` bash
yay -S mcpelauncher-linux mcpelauncher-ui
```

#### Run

You can find it in the startmenu or run the following command

``` bash
mcpelauncher-ui-qt
```

If it doesn't start you can enable debug logging like this

``` bash
mcpelauncher-ui-qt -v
```

## macOS

<div class="warning">

Mojang will soon require OpenGL ES 3.1

Starting with March 2025 updates to Minecraft can stop in this macOS Port, which supports at most OpenGL ES 3.0

It's not recommend to buy the android game just for this launcher

</div>

Prebuilt **macOS binary's** are [currently available
here](https://github.com/ChristopherHX/osx-packaging-scripts/releases/latest).
Always copy the App to a writeable location otherwise the updater won't
work.

## Source build

If there are no packages available for your distribution or you want to compile, check out the
[Source Build](../source_build/index.md) guide.
