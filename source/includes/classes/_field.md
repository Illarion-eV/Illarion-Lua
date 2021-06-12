## Field

`Field`s make up the game map. `Character`s stand on `Field`s, `Item`s are on `Field`s, warps make `Player`s jump from
one Field to another. Each Field is on a different logical `position`.

### Functions

Most of the time these functions will be used on a `Field` received from `world:getField(position)`.

```lua
local field = world:getField(user.pos)
local id = field:tile()
```
#### `number tile()`

Returns the tile id of that `Field`, meaning the number for "water", "grass", etc.

#### `number countItems()`

Returns the number of `Item`s on top of that `Field`.

#### `Item getStackItem(number stackPosition)`

Returns the `Item` at `stackPosition` on a given `Field`. `stackPosition == 0` will return the bottom `Item`.
If `stackPosition` is equal or greater than the number of `Item`s on that field, an `Item` with id `0` will be returned.

#### `boolean isPassable()`

Determines whether or not a `Field` allows a `Character` to pass over it or having `Item`s dropped on it.

#### `boolean, position isWarp()`

Returns whether or not a `Field` is a warp as well as the warp destination.

#### `setWarp(position destination)`

Enables the `Field`'s warp and sets its `destination`.

#### `removeWarp()`

Removes the `Field`'s warp.