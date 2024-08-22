# Troubleshooting

::: contents

local

:   
:::

## Extracting APKs

### I downloaded a Minecraft APK from the internet and it doesnt work!

APKs acquired from anything other than the Google Play store is
unsupported by us. It might be possible, but we will not help you.

### I copied the Minecraft APK from my phone over to my computer, but it doesnt extract

Your APK is made for the ARM architecture. You need an x86 (32-bit) or
x86_64 (64-bit) APK to play on your computer. If you have an ARM laptop
(most chromebooks, pinebook) it should work.

### Can somebody give me the APK / extracted files?

**NO.** That is Piracy and we **DO NOT** support it on this project.
Anyone caught asking this in the support server will face consequences.

## AppImage

### AppImage UI to large

Scaling of qt5 in our AppImages is broken on some pc\'s. Here a
workaround

``` bash
QT_SCALE_FACTOR=1 QT_AUTO_SCREEN_SCALE_FACTOR=0 ./MC.AppImage
```

Make shure to replace `./MC.AppImage` with the actual path to your
AppImage file. On most systems you can drag\'n drop the AppImage from
your file manager into the Terminal window to enter the full path.

Source:
<https://github.com/ChristopherHX/mcpelauncher-ui-manifest/issues/9>

## Controller

### The player\'s view drifts by itself when a controller is plugged in

This happens when the controller\'s Deadzones are not set properly for
the game. You must manually set the deadzones for your controller.

-   Linux:
    <https://wiki.archlinux.org/index.php/Gamepad#evdev_API_deadzones>
    or if you have an Xbox360 Controller, open a terminal and run
    `sudo xboxdrv --detach-kernel-driver --deadzone 6000 --silent --type xbox360 --mimic-xpad`
    while you are **ingame**.
-   Mac OS X: TBA

### The controller doesn\'t work at all or you want to remap your gamepad buttons, analogsticks, dpad and triggers?

You need to create a gamepadmapping for your unknown gamepad.

-   Download <https://generalarcade.com/gamepadtool/>
-   create a mapping with it
-   copy the new mapping line into
-   AppImage: `~/.local/share/mcpelauncher/gamecontrollerdb.txt`
-   Flatpak:
    `~/.var/app/io.mrarm.mcpelauncher/data/mcpelauncher/gamecontrollerdb.txt`
-   macOS:
    `~/Library/Application Support/mcpelauncher/gamecontrollerdb.txt`
-   you have to create this text file, if it doesn\'t exist
-   reopen the game

**The launcher can detect this situation, but it has been disabled to
notify the user, because peoples mice, keyboards etc. were detected as
gamepads**, how broken some linux systems are is a mystery.

Your gamepad driver might be incompatible, then you need a sane
controller.

Under Linux, you may have to plug the controller **after** launching the
game.

## Game launcher

### Graphics performance issues (software rendering) - `EGLUT: failed to initialize EGL display...`

If the game is running poorly, it might be using software rendering
(identified by the `llvmpipe` string in the renderer). If you have been
redirected here by a link in the launcher this is the case.

You should make sure to install the proper 32-bit graphic drivers for
your hardware.

-   For integrated graphics and most AMD GPUs (and maybe Nvidia on
    nouveau) -
    `sudo apt-get install libegl1-mesa:i386 libegl1-mesa-drivers:i386`
-   For some Nvidia cards (eg. GeForce series), assuming proprietary
    driver is already installed, install the associated libnvidia-gl-xxx
    package (where xxx = driver version for your hardware). For example,
    if the nvidia-driver-390 metapackage is installed, then
    `sudo apt-get install libnvidia-gl-390`.

You may need to reinstall the proprietary drivers if you had installed
them manually before.

### Black screen with Mesa 23.1+

Try adding `MESA_EXTENSION_OVERRIDE=-GL_EXT_instanced_arrays` to
environment variables.

### MSA daemon could not be found

Make sure you have properly installed the following packages:
`msa-daemon msa-ui-qt` If compiling from sources, make sure to install
the MSA component.

### No audio / music

**❗Please note that the in-game Music is downloaded separately as a
free item in the Marketplace.❗**

-   **Ubuntu:** Make sure `libasound2:i386` is installed. If it is, you
    may need to install `libpulse0:i386`.
-   **Arch:** Make sure `lib32-libpulse` and `lib32-alsa-plugins` are
    installed on your system.
-   **Other distros:** Make sure to install alsa (asound) and/or
    pulseaudio depending on your system configuration.
-   **macOS:** The macOS i386 launcher doesn\'t have a recent enough
    native libfmod.so file for Minecraft

PipeWire: - **Ubuntu, Arch**: Make sure `pipewire-alsa` is installed. -
**Gentoo**: Make sure the `pipewire-alsa` USE flag is set for the
`pipewire` package. - **Other distros**: Make sure to install the
PipeWire ALSA plugin depending on your system configuration.

### Updating the launcher {#updating_the_launcher}

-   Linux AppImage or macOS to update the launcher on newer versions of
    the launcher, press the gear icon and then check for updates
-   Flatpak `sudo flatpak update`

If your launcher is too old or you can\'t find these buttons, you may
need manually download a newer AppImage (Linux) or MacOS binary.

### MacOS X Catalina

Should be solved by
`updating the launcher <updating_the_launcher>`{.interpreted-text
role="ref"}

### Google prevents login `This browser or app may not be secure. Try using a different browser`

Should be solved by
`updating the launcher <updating_the_launcher>`{.interpreted-text
role="ref"}

### File picking doesn\'t work or crashes

You need to install the `zenity` utility:

-   Debian/Ubuntu - `sudo apt-get install zenity`

### I compiled and/or installed everything, but Minecraft doesn\'t start

Chances are, you don\'t have the actual game yet. This project does
**not** provide MCPE/Minecraft Bedrock Edition itself.

The easiest way to download and start the game is through the graphical
Qt UI (`mcpelauncher-ui-qt`, sometimes called metalauncher). This
requires to log into a Google Play Account with Minecraft purchased.

Otherwise, obtain a valid Minecraft x86 `.apk` file and use the
`extract utility <extractor>`{.interpreted-text role="ref"}.

### I used the Qt UI (metalauncher) to download the game, but `mcpelauncher-client` still doesn\'t work

To start a given version of Minecraft you can run `mcpelauncher-client`
with the `-dg` argument, eg.
`mcpelauncher-client -dg ~/.local/share/mcpelauncher/versions/DESIRED_VERSION`.

`ls ~/.local/share/mcpelauncher/versions/` will list all versions you
have installed.

### I run into lagspikes during gameplay

This can be fixed by starting the game manually via the command line. To
do this, open a terminal and run the following:

Linux:

-   `mcpelauncher-client -dg ~/.local/share/mcpelauncher/versions/1.2.3.4` -
    Replace 1.2.3.4 with the version of Minecraft you want to run.

Mac OS X:

-   `cd /Applications/Minecraft\ Bedrock\ Launcher.app/Contents/MacOS`
-   `./mcpelauncher-client -dg ~/Library/Application\ Support/mcpelauncher/versions/1.2.3.4` -
    Replace 1.2.3.4 with the version of Minecraft you want to run.

## Qt launcher UI

### Running the troubleshooter

Click the gear icon (settings) in the top right corner of the Qt
launcher window, and press the \[Run troubleshooter\] button.

### Could not find the game launcher

This may happen when the game launcher has not been installed or set
properly. The launcher (mcpelauncher-client) must be available in the
PATH variable for the launcher to work. If you are compiling from
sources and do not want to install the launcher, please set the
GAME_LAUNCHER_PATH at compile time with cmake (eg.
`cmake -DGAME_LAUNCHER_PATH-/home/paul/mcpelauncher/build/mcpelauncher-client ..`,
make sure that this is the path to the directory containing the binary,
and not the binary itself). Otherwise make sure the launcher is properly
installed in your system.

### The launcher crashes when I press Download and Play

First of all, make sure a version name is displayed under the Download
and Play button. If it\'s not, please wait some time and/or try
restarting the launcher. A window asking you to accept Google Play TOS
should appear first.

If the launcher still fails to download, it\'s possible you are trying
to download a beta version of the game. Make sure to register in the
beta first at
<https://play.google.com/apps/testing/com.mojang.minecraftpe>.

**You must have purchased Minecraft on the account you\'re trying to
use.**

In some cases, you may need to
`clear the launcher data <clearing_the_launcher_ui_data>`{.interpreted-text
role="ref"}.

### Clearing the launcher UI data {#clearing_the_launcher_ui_data}

Run the following commands:

``` bash
rm -rf ~/.config/Minecraft\ Linux\ Launcher
rm -rf ~/.local/share/Minecraft\ Linux\ Launcher
rm -rf ~/.cache/Minecraft\ Linux\ Launcher
```

### Obtaining the game log

In order to be able to view the game log, in the launcher press the gear
in the top right corner and check the \"Show log when starting the
game\" option. This will show a log and update it in realtime. You can
copy it by pressing the icon in the top-right corner of the log window.
Additionally, the log will be shown if the game crashes.
