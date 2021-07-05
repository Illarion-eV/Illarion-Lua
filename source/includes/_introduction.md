# Introduction

Illarion game content like items, NPCs, quests, etc. is defined in scripts written in
<a target="_blank" rel="noopener noreferrer" href='https://www.lua.org/manual/5.2/'>Lua 5.2</a>
with Illarion specific extensions. This document describes these extensions. Those scripts can be found in the
<a target="_blank" rel="noopener noreferrer" href='https://github.com/Illarion-eV/Illarion-Content'>
official repository</a>, which has two branches. The `master` branch reflects the scripts used by the live game, while
the `develop` branch is used to prepare the next release. You can fork that repository on GitHub and clone it to your
hard drive for development or testing using the
<a target="_blank" rel="noopener noreferrer" href='https://github.com/Illarion-eV/Illarion-Dev'>
local development server</a>.

The recommended editor for Illarion scripting is
<a target="_blank" rel="noopener noreferrer" href='https://code.visualstudio.com/'>
Visual Studio Code</a>, which is available for Linux, Windows and macOS. You can use the extension `rog2.luacheck` to
automatically perform some code checks ahead of pull requests. If you are using Visual Studio Code and open the
repository directory as a folder, the required ISO 8859-1 encoding will be used automatically. A more detailed
description of setting up and using a development environment is available in the [tutorial](#tutorial).

<aside class="notice">
Scripts need to be encoded in ISO 8859-1.
</aside>

## Learning Lua

If you are new to programming in general or new to Lua, you will need to learn Lua 5.2 if you want to make changes
beyond searching for and fixing text errors. Luckily Lua is a fairly simple language and I would suggest beginning by
studying [Programming in Lua](https://www.lua.org/pil/contents.html) chapters 1 to 5.1. You can skip 1.4, since we won't
be using a stand-alone interpreter, but rather our [local Illarion server](https://github.com/Illarion-eV/Illarion-Dev).
While this book is geared towards Lua 5.0, the basics did not change. Before you get started, make sure to follow the
[tutorial](#tutorial) to set up a development environment.

> Minimal script for testing Lua code

```lua
local M = {}

function M.UseItem(user, item, actionState)
    -- your code here
end

return M
```

While learning, you will want to test your code snippets. To do that, you can go to an item script of your choosing,
e.g. `item/id_9_saw.lua` and delete all of its contents. Then paste the example on the right and write your code inside
the `UseItem` entry point. Make sure to reload (`!fr` in the client) the server after saving your script to load any
changes. Now you can run your code by simply using that item. To create an item with e.g. id 9, use `!create 9` in your
client (the item might be created in your bag).

Since `print` does not exist here (where would we print output anyway), you need to use another means of producing
output. You can either use `debug("some output text")` to send output to the server log, or use
`user:inform("some output text")` to send output to your client.

If you struggle or are not sure about something, you are always welcome to ask for help in [Discord]
(https://illarion.org/community/us_chat.php). Developers will be notified if you use the channel Development >
beginners.

## Structure

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
<li>Directory/file names are separated by a full stop (<code>.</code>).</li>
<li>The <code>.lua</code> extension is omitted.</li>
</ul>
E.g. a script <code>item/apple.lua</code> would be entered as <code>item.apple</code>.
</aside>

The executed function is called an [_entry point_](#entry-points), since it is run directly by the server. Scripts
defined in the database, as well as server scripts, return a table containing expected entry points.
A script does not need to include _all_ possible entry points. For example, if an item has no `UseItem` entry point,
nothing happens when a player uses the item.

<aside class="notice">
The available set of entry points describes all game behaviour scripts can handle.
</aside>

## Database Changes

```sql
INSERT INTO triggerfields VALUES (330, 536, -24, 'triggerfield.irundarmirror');
INSERT INTO npc VALUES (2, 61, 334, 538, -26, 0, false, 'Neil Peter Caldori', 'npc.caldori');
UPDATE items SET itm_script = 'item.food' WHERE itm_id = 15;
```
> In the second example everything after npc_script will get a default value. You probably do not want an NPC with white skin, though.

You need to track all changes you make to the database. This will allow you to

* replay any changes if you need to reset your database to incorporate changes to the official database.
* have a changeset to include in your pull request for testing and to update the official database upon merging.

To apply your changes easily, you need to write them down in SQL. Typically these will be INSERT statements for new
database entries (new NPCs, quests, trigger fields, ...) and UPDATE statements for modifying existing entries
(e.g. adding a script to an item). The syntax is pretty simple:

`INSERT INTO <table name> VALUES (<list of all required values>);`

`UPDATE <table name> SET <field name> = <value> WHERE <id field> = <entry id>;`

<aside class="notice">
Helpful hints for crafting SQL statements:
<ul>
<li>Database access is explained in the <a target="_blank" rel="noopener noreferrer" href='https://github.com/Illarion-eV/Illarion-Dev#7-database-access'>local server documentation</a>.</li>
<li>Strings are put in single quotes (<code>'</code>).</li>
<li>Possible boolean values are <code>true</code> and <code>false</code>.</li>
<li>If no value should be inserted for some field, use <code>NULL</code>.</li>
<li>You can omit the last values in an INSERT statement if they all have default values.</li>
<li>Do not forget the semi-colon after each SQL statement.</li>
</ul>
</aside>

<aside class="notice">
You can run your set of SQL statements against your local database after clicking "SQL" in the top right corner of
phppgadmin.
</aside>
## Notation

Function definitions in this document are given in the following format:

`<return values> <function name>(<parameters>)`

* `return values` stands for a list of variables returned from the function and is omitted if the function does not
return anything.
* `<function name>` is the name of the function.
* `<parameters>` is a list of type/name pairs, separated by space. Optional parameters are given in brackets.
  Default parameters are assigned the value they will be given if left out of a call.

Example:

`weight, value example(Item item [, number amount = 1])`

The function `example` given here returns `weight` and `value`. It takes an `Item` called `item` as well as an optional
`number` called `amount` as parameters. If `amount` is not passed into the function it will be set to `1`.