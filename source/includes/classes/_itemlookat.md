## ItemLookAt

Holds information about an item which is used by the client to display item inspection pop-ups. It is mainly used in the
[server entry point](#server) `lookAtItem` and the [Item entry point](#items) `LookAtItem`.

### Variables

```lua
local itemLookAt = ItemLookAt()
itemLookAt.name = "Sword"
itemLookAt.rareness = ItemLookAt.uncommonItem
```

All variables are writable.

Name            | Type    | Default                 | Description
--------------- | ------- | ----------------------- | -----------
name            | text    | `""`                    | item name, _must_ be set
rareness        | number  | `ItemLookAt.commonItem` | has to be one of ItemLookAt.commonItem, ItemLookAt.uncommonItem, ItemLookAt.rareItem, ItemLookAt.epicItem
description     | text    | `""`                    | item description
craftedBy       | text    | `""`                    | who crafted the item
type            | text    | `""`                    | states what kind of item this is
level           | number  | `0`                     | item level from 0 to 100
usable          | boolean | `true`                  | can the item be used by players?
weight          | number  | `0`                     | item weight
worth           | number  | `0`                     | selling price (to NPCs) in copper coins
qualityText     | text    | `""`                    | describing item quality
durabilityText  | text    | `""`                    | describing item durability
durabilityValue | number  | `0`                     | from 0 to 100 in percent
diamondLevel    | number  | `0`                     | magic gem level from 0 to 10
emeraldLevel    | number  | `0`                     | magic gem level from 0 to 10
rubyLevel       | number  | `0`                     | magic gem level from 0 to 10
sapphireLevel   | number  | `0`                     | magic gem level from 0 to 10
amethystLevel   | number  | `0`                     | magic gem level from 0 to 10
obsidianLevel   | number  | `0`                     | magic gem level from 0 to 10
topazLevel      | number  | `0`                     | magic gem level from 0 to 10
bonus           | number  | `0`                     | gem bonus from 0 to 255

### Functions

#### `ItemLookAt()`

Returns new ItemLookAt with default values.

