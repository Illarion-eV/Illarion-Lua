# Introduction

Illarion game content like items, npcs, quests, etc. is defined in scripts written in
[Lua 5.2](https://www.lua.org/manual/5.2/) with Illarion specific extensions. This document describes these extensions.
Those scripts can be found in the [official repository](https://github.com/Illarion-eV/Illarion-Content), which has two
branches. The `master` branch reflects the scripts used by the live game, while the `develop` branch is used to prepare
the next release. You can fork that repository on GitHub and clone it to your hard drive for development or testing
using the [local development server](https://github.com/Illarion-eV/Illarion-Dev).

The recommended editor for Illarion scripting is [Visual Studio Code](https://code.visualstudio.com/), which is
available for Linux, Windows and macOS. You can use the extension `rog2.luacheck` to automatically perform some code
checks ahead of pull requests. If you are using Visual Studio Code and open the repository directory as a folder,
the required ISO-8859-1 encoding will be used automatically. A more detailed description of setting up and using a
development environment is available in the [tutorial](#tutorial).

<aside class="notice">
Scripts need to be encoded in ISO-8859-1.
</aside>

> `item/apple.lua`

```lua
-- mandatory license header omitted for the sake of brevity

local M = {}

function M.UseItem(user, item)
    -- code handling items being used
end

function M.LookAtItem(user, item)
    -- code handling items being looked at
end

-- more entry points can follow

return M
```

Every time a certain event happens (e.g someone using an item, a monster dying, someone logging into the game, etc.) a
script function is called. The name of that script is usually defined in the database, except for _server
scripts_ which have a fixed name and implement very specific server behaviour not tied to a particular game object.

<aside class="notice">
Scripts are defined inside the database using the following format:
<ul>
<li>Paths are relative to the repository base directory.</li>
<li>Directory/file names are seperated by a full stop (<code>.</code>).</li>
<li>The <code>.lua</code> extension is omitted.</li>
</ul>
E.g. a script <code>item/apple.lua</code> would be entered as <code>item.apple</code>.
</aside>

The executed function is called an [_entry point_](#entry-points), since it is run directly by the server. Scripts
defined in the database, as well as server scripts, return a table containing expected entry points.
A script does not need to include _all_ possible entry points. For example, if an item has no `LookAtItem` entry point,
nothing special happens when a player inspects the item.

