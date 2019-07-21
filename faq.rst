Frequently Asked Questions
==========================

Does it work on Windows 7 / 8?
~~~~~~~~~~~~~~~~~~~~~~~~
No, due to the amount of work required to get this running on Windows. Play the Windows 10 Edition instead if you can.
Note that you can not run this in the current version of `Windows Subsystem for Linux (WSL) <https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux>`__, as it does not support 32-bit applications.

How does it work?
~~~~~~~~~~~~~~~~~
The project runs the native libraries from the Android version directly on your computer. This is accomplished by fixing the incompatibilities between the libc used on Android and the one used on desktop Linux or OS X (Android - Bionic; Linux - glibc). This is a simple compatibility layer which doesn't impact performance in any significant way; it's similar to Wine in a way, but way more lightweight and simple. Aditionally, all Android-specific code has been rewritten to run on Linux (AppPlatform, Store, Xbox Live, etc.).

I compiled and/or installed everything, but :code:`mcpelauncher-client` doesn't start
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Chances are, you don't have the actual game yet. This project does **not** provide MCPE/Minecraft Bedrock Edition itself.

The easiest way to download and start the game is through the graphical Qt UI (:code:`mcpelauncher-ui-qt`, sometimes called metalauncher). This requires to log into a Google Play Account with Minecraft purchased.

Otherwise, obtain a valid Minecraft x86 :code:`.apk` file and use the :ref:`extract utility <extractor>`.

I Used the Qt UI (metalauncher) to download the game, but :code:`mcpelauncher-client` still doesn't work
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To start a given version of Minecraft you can run :code:`mcpelauncher-client` with the :code:`-dg` argument, eg. :code:`mcpelauncher-client -dg ~/.local/share/mcpelauncher/versions/DESIRED_VERSION`.

:code:`ls ~/.local/share/mcpelauncher/versions/` will list all versions you have installed.

Where are my worlds?
~~~~~~~~~~~~~~~~~~~~
Linux: :code:`~/.local/share/mcpelauncher/games/com.mojang/minecraftWorlds`

Mac OS X: :code:`~/Library/Application Support/mcpelauncher/games/com.mojang/minecraftWorlds`

Each world has its own directory. If you have multiple worlds, you can identify them by their name in :code:`levelname.txt` found in each world.

The :code:`mcpelauncher-server` creates and expects its world files in :code:`world`.

Can I use resource packs?
~~~~~~~~~~~~~~~~~~~~~~~~~
Yes, put them in :code:`~/.local/share/mcpelauncher/games/com.mojang/resource_packs`.

For Mac OS X, put them in :code:`~/Library/Application Support/mcpelauncher/games/com.mojang/resource_packs`.

Shaders are also resource packs. (Shaders must be GLSL based)

You may need to extract :code:`.zip` and :code:`.mcpack` files into their own subdirectory for them to work properly.

Why would I want to use this projects server, instead of the official one?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If...

- the official one doesn't work for you
- you need scripting on the server
- some rarely needed particular modding capabilities

How can I get capes? / Can I install capes?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Yes, you can get capes; first go to the link `Minecraft Capes Pack <https://www.mediafire.com/file/4je935z6ki94j6v/Capes_1.7%252B_%2528PatarHD%2529.zip/file>`_

After downloading the file, Open it and go to :code:`vanilla`.

All the required files will be there.If you want to add your own custom skin,Put it in the :code:`vanilla` folder but **DO NOT** delete the :code:`nitrosfn.png`skin or the :code:`alex.png`skin.

If you want to change the cape,go to the other folder :code:`cape presets`and name the cape you want:code:`cape.png`and then place it in the :code:`vanilla`folder and replace the cape that is currently in the folder

If you want a custom cape, make sure it is a 64x32 pixel cape otherwise it will not work.

Now,in a seperate finder folder, go to the directory :code:`~Library/Application Support/versions` then go to the folder which shows the version of minecraft you run.

After, go to :code:`assets` then go to :code:`skin_packs` then :code:`vanilla`.

From the other finder, where your custom cape and skin is, copy all the files and post it in the :code:`vanilla` where your default minecraft files are and replace the default files with the new ones.

Open the new :code:`skin.json` file with text edit and look for :code:`
{
  "skins": [
    {
      "localization_name": "Steve",
      "geometry": "geometry.humanoid.custom",
      "texture": "nitrosfn.png",
	  "cape": "cape.png",
      "type": "free"`.
      
      Change the :code:`nitrosfn.png` to the name of the custom skin you use.
      
      Now save and exit, restart your launcher and launch it and when you go to the skin section, your skin should have a cape.

