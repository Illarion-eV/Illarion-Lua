## Field

Fields make up the game map. Characters stand on fields, items are on fields, warps make players jump from
one field to another. Each field is on a different logical `position`.

### Functions

Most of the time these functions will be used on a field received from `world:getField(position)`.

```lua
local field = world:getField(user.pos)
local id = field:tile()
```
#### `number tile()`

Returns the tile id of that field, meaning the number for "water", "grass", etc.

#### `number countItems()`

Returns the number of items on top of that field.

#### `Item getStackItem(number stackPosition)`

Returns the item at `stackPosition` on a given field. `stackPosition == 0` will return the bottom item.
If `stackPosition` is equal or greater than the number of items on that field, an item with id `0` will be returned.

#### `boolean isPassable()`

Determines whether or not a field allows a character to pass over it or having items dropped on it.

#### `boolean, position isWarp()`

Returns whether or not a field is a warp as well as the warp destination.

#### `setWarp(position destination)`

Enables the field's warp and sets its `destination`.

#### `removeWarp()`

Removes the field's warp.