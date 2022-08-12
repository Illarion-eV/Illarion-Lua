# GM Commands

GM commands are server commands that admin characters have access to. Some if not all of these could prove useful for testing purposes.
A lot of additional functionality not included by these commands is in the GM tool kit(Item IDs: 93, 99, 100, 382).

If your local test-character does not have permissions to use these commands, this can be altered in your local database.

All GM commands are prefixed with an exclamation (!) mark.

#### `!?`
Provides an in-game list of the commands you have permission to make use of.

#### `!create [itemID/itemName] [quantity] [quality] [dataKey = dataValue]`

Creates an item in your inventory, provided there is sufficient inventory slots and you are not overencumbered.

Example:

!create pickaxe 2 899 nameEn=Apple nameDe=Apfel

The above would create two brand new pickaxes of excellent quality, both with the custom name Apple/Apfel(depending on the perusing players client language).

A list of itemIds can be found in [resources.](#resources)

#### `!jumpto(!j) [player]`

Teleports you to the player.

Example:

!jumpto Brightrim

#### `!warp_to(!w) [x] [y] [z]`

Warps you to the given coordinates.

Example:

"!w 701, 285, 0" would take you to the new player spawn in Troll's Haven.

#### `!what`

POrovides you information about the position, tile, topmost item and character belonging to the field in front of you.

#### `!who [player]`

If left blank, this command lists all players online, with player/admin status and character ids.

If a player is specified, it also provides the position, health status and chosen language of the player.

#### `!forceintroduce(!fi) [charId/charName]`

Introduces the character to all GM characters in range.

#### `!forceintroduceall(!fia)`

Introduces all characters in sight to you.

#### `!talkto(!tt) [charName], [message]`

Sends a message to the specified character.

Example:

!tt Brightrim, This is my message for Brightrim

#### `!broadcast(!bc) [message]`

Sends a broadcast to all online players.

Example:

!bc The server will go down for maintenance soon.

#### `!add_teleport [x] [y] [z]`

Adds a teleport field from your position to the designated coordinates.

#### `!showwarpfields [range]`

Lists all the warp fields within the specified range, if any exist.

#### `!removewarpfield [x] [y] [z]`

Remove the warp field on the given position, if one exists.

#### `!summon(!s) [charName]`

Teleport the designated character to your position.

#### `!ban(!b) [charName]`

Bans the designated character indefinitely.

This only bans the specific character, not the players account or other characters.

#### `!spawn [monsterId]`

Spawns a monster of the given ID next to you.

The GM tools do this much better, allowing you to also designate the amount of monsters to spawn.

Example:

"!spawn 5" would spawn a human thief.

#### `!kick(!k) [charName]`

Kicks the specified character from the game.

#### `!kickall(!ka)`

Kick all players out of the game.

#### `!mapsave`

Saves the map after changes were made.

#### `!fullreload(!fr)`

Reloads all the scripts and database tables.

Without this, any changes to the database or scripts is not reflected in the game.

#### `!nuke`

Kills all monsters on the map.

#### `!makevisible(!mv) / !makeinvisible(!mi)`

Turns your characters (in)visible.

#### `!exportmaps`

Exports the current maps.

#### `!login [boolean]`

Changes whether players can login. When set to false, only GMs can log in.

#### `!create_area [x] [y] [z] [width] [height] [tileId]`

Creates a new map at the given location of the given width and height, filled with tiles of the given tileId.

Example:

"!create_area 0 0 5 10 10 5" would create a 10 by 10 field of lava on the 5th layer above the testing area(0,0,0) of the map.

A list of available tileIds can be found in [resources.](#resources)

#### `!set_spawn [boolean]`

(De)activates the spawning of monsters. If set to false, monsters will no longer spawn on the map until it is turned back on.

#### `!playersave(!ps)`

Saves all players to the database.

#### `!clippingoff(!coff) / !clippingon(!con)`

Turns clipping on/off. If it is off, you can walk through normally solid objects or unwalkable tiles.

#### `!tile(!t) [tileId]`

Changes the tile in front of you to the given tileId.

A list of available tileIds can be found in [resources.](#resources)

#### `!turtleon(!ton) [tileId] / !turtleoff(!toff)`

When turned on, any tile you walk on will be turned into the given tileId.

A list of available tileIds can be found in [resources.](#resources)

