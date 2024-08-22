# Dedicated server {#server}

Last updated to work with 1.12.0.28 and 1.12.1.1, other versions won\'t
work. If you want to use a specific Minecraft version you\'ll need to
start the mcpelauncher-server with the [-dg]{.title-ref} argument,
pointing to the directory in which Minecraft was extracted using
`the extract utility <extractor>`{.interpreted-text role="ref"} or using
the Qt UI launcher.

:::: note
::: title
Note
:::

When using the Qt UI use the following command line option to select the
game version (replace 1.2.3.4 with the version you want to use):

-   On Linux: `-dg ~/.local/share/mcpelauncher/versions/1.2.3.4`
-   On MacOS: `-dg ~/Library/Application\ Support/versions/1.2.3.4`
::::

## Server Properties

The dedicated server is configurable using a server.properties file with
a syntax similar to the one used in the desktop Minecraft
([key=value]{.title-ref}).

:::: note
::: title
Note
:::

The server automatically saves a default `server.properties` file the
first time it is started in the data directory (which is
`~/.local/share/mcpelauncher/` by default; it can be overridden using
the `-dd` command line option).
::::

### Supported properties

-   `level-dir` (recommended to set) - name of the world in
    games/com.mojang/minecraftWorlds. An empty name will cause the world
    to be saved directly in the root worlds directory and can cause
    issues with saving.
-   `level-name` - name of the world
-   `level-generator` - the world generator (0 - old, 1 - infinite, 2 -
    flat)
-   `level-seed` - world seed
-   `difficulty` - difficulty level (default: 0 - peaceful)
-   `gamemode` - default gamemode (default 0 - survial)
-   `force-gamemode` - whether the gamemode should be enforced for
    existing players on join (default: false)
-   `motd` - Message of the Day, displayed on the server list (has to be
    set for the server to be shown on the LAN world list, default:
    empty)
-   `server-port` - port (default: 19132)
-   `server-port-v6` - port for IPv6 connections (default: 19133)
-   `max-players` - maximal player count on the server (default: 20)
-   `online-mode` - specifies whether Xbox Live login is required to
    join the server (default: true)
-   `view-distance` - maximal supported view distance (default: 22)
-   `player-idle-timeout` - timeout in minutes after which players will
    be disconnected. Unlike the desktop edition, this value supports
    real numbers; (default: 0 - no timeout)

### Example of a custom [server.properties]{.title-ref} file

``` bash
level-dir=world
level-name=My World
level-generator=1
level-seed=21389432043234
difficulty=0
gamemode=1
force-gamemode=false
motd=§eMy Minecraft server
server-port=19132
server-port-v6=19133
max-players=100
online-mode=false
view-distance=22
player-idle-timeout=0
```
