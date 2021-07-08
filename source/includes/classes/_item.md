## Item

```lua
item.quality = 284
item.setData("name", "John's Item")
world:changeItem(item)
```
Represents an actual item on the map or in a character's pockets. If you change an `item`, you need to propagate your
changes to the server via `world:changeItem(item)`.
### Constants

```lua
local itemStats = world:getItemStatsFromId(Item.apple)
```
If an item has an entry `someUniqueItemName` in `itm_name` in the item's database entry, you can get its id with
`Item.someUniqueItemName`. This is more descriptive than using the actual number.

### Variables

Name    | Type      | Writable  | Description
--------| --------- | --------- | -----------
id      | number    | yes       | item id
inside  | Container | no        | if the item is in a container, this is that container
itempos | number    | no        | if the item is in a container or in a character's inventory, this is its position there
number  | number    | yes       | number of identical items in the stack
owner   | Character | no        | if the item is on a character, this is that character
pos     | position  | no        | if the item is on the map, this is the position of the field it is on
quality | number    | yes       | item quality from 0 to 999, where the first digit is quality and the last two digits are durability
wear    | number    | yes       | if an item can decay it loses one wear point every three minutes

### Functions

#### `string getData(string key)`
```lua
local prayerLevel = tonumber(item:getData("prayerLevel"))
```
Returns the item's data value for the given `key` if that key exists and an empty string otherwise.

#### `number getType()`
```lua
if item:getType() == scriptItem.field then
    debug("item with id " .. item.id .. " is on the ground")
end
```

Depending on where the item is located, will return one of

* `scriptItem.notdefined`
* `scriptItem.field`
* `scriptItem.inventory`
* `scriptItem.belt`
* `scriptItem.container`

#### `boolean isLarge()`
```lua
local blocksView = item:isLarge()
```
Returns true if and only if the item is large enough to block a character's view. This means in the database it has a
volume of at least 5000.

#### `setData(string key, number value)`
#### `setData(string key, string value)`
```lua
item:setData("prayerLevel", 12)
item:setData("prayerLevel", "")
item:setData("prefix", "very strong ")
```
> The second line removes the data key `prayerLevel` from the item.

Sets the data `value` for a given `key` unless `value` is an empty string, in which case the entry for `key` is removed.
If given a number for `value`, that number is stored as the corresponding string.