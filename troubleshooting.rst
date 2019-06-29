Troubleshooting
===============

.. contents:: :local:

Appimage
--------

Appimage crashes when I try to sign in to Google
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The current workaround is to use LD_PRELOAD for nss3, eg. :code:`LD_PRELOAD=/usr/lib/libnss3.so ./Minecraft_Bedrock_Launcher.AppImage`

Game launcher
-------------

Graphics performance issues (software rendering)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the game is running badly, it might be using software rendering (identified by the :code:`llvmpipe` string in the renderer). If you have been redirected here by a link in the launcher this is the case.

You should make sure to install the proper 32-bit graphic drivers for your hardware.
- For integrated graphics and most AMD GPUs (and maybe Nvidia on nouveau) - :code:`sudo apt-get install libegl1-mesa:i386 libegl1-mesa-drivers:i386`
- You may need to reinstall the proprietary drivers if you had installed them manually before.

MSA daemon could not be found
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Make sure you have properly installed the following packages: :code:`msa-daemon msa-ui-qt`
If compiling from sources, make sure to install the MSA component.

No audio
~~~~~~~~
- **Ubuntu:** Make sure :code:`libasound2:i386` is installed. If it is, you may need to install :code:`libpulse0:i386`.
- **Other distros:** Make sure to install alsa (asound) and/or pulseaudio depending on your system configuration.

.. _updating_the_launcher:

Updating the launcher
~~~~~~~~~~~~~~~~~~~~~
Depending on your system the process may vary:
- Ubuntu prebuilt packages - :code:`sudo apt-get update && sudo apt-get upgrade`
- Mac OS - Redownload the package

1.8 does not work and crashes with :code:`failed to locate madvise`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Make sure to :ref:`update the launcher <updating_the_launcher>`. If you have switched from using a source build to a binary one, :ref:`make sure to uninstall the source one first <source_uninstall>`.

File picking doesn't work or crashes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
You need to install the :code:`zenity` utility:
- Ubuntu - :code:`sudo apt-get install zenity`

I run into lagspikes during PvP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This can be fixed by starting the game manually via the command line. To do this, open a terminal and do the following:

Linux:

- :code:`mcpelauncher-client -dg ~/.local/share/mcpelauncher/versions/1.2.3.4` - Replace 1.2.3.4 with the version of Minecraft you want to run.

Mac OS X:

- :code:`cd /Applications/Minecraft\ Bedrock\ Launcher.app/Contents/MacOS`
- :code:`./mcpelauncher-client -dg ~/Library/Application\ Support/mcpelauncher/versions/1.2.3.4` - Replace 1.2.3.4 with the version of Minecraft you want to run.

Qt launcher UI
--------------

Running the troubleshooter
~~~~~~~~~~~~~~~~~~~~~~~~~~
Click the gear icon (settings) in the top right corner of the Qt launcher window, and press the [Run troubleshooter] button.

Could not find the game launcher
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This may happen when the game launcher has not been installed or set properly. The launcher (mcpelauncher-client) must be available in the PATH variable for the launcher to work.
If you are compiling from sources and do not want to install the launcher, please set the GAME_LAUNCHER_PATH at compile time with cmake (eg. :code:`cmake -DGAME_LAUNCHER_PATH-/home/paul/mcpelauncher/build/mcpelauncher-client ..`, make sure that this is the path to the directory containing the binary, and not the binary itself). Otherwise make sure the launcher is properly installed in your system.

The launcher crashes when I press Download and Play
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
First of all, make sure a version name is displayed under the Download and Play button. If it's not, please wait some time and/or try restarting the launcher. A window asking you to accept Google Play TOS should appear first.

If the launcher still crashes, it's possible you are trying to download a beta version of the game. Make sure to register in the beta first at https://play.google.com/apps/testing/com.mojang.minecraftpe.

You must have purchased Minecraft on the account you're trying to use.

In some cases, you may need to :ref:`clear the launcher data <clearing_the_launcher_ui_data>`.

.. _clearing_the_launcher_ui_data:

Clearing the launcher UI data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run the following commands:

.. code:: bash

   rm -rf ~/.config/Minecraft\ Linux\ Launcher
   rm -rf ~/.local/share/Minecraft\ Linux\ Launcher
   rm -rf ~/.cache/Minecraft\ Linux\ Launcher

Obtaining the game log
~~~~~~~~~~~~~~~~~~~~~~
In order to be able to view the game log, in the launcher press the gear in the top right corner and check the "Show log when starting the game" option. This will show a log and update it in realtime. You can copy it by pressing the icon in the top-right corner of the log window.
Additionally, the log will be shown if the game crashes.
