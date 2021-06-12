### Movement/Position functions

#### `move(number direction, boolean activeMove=true)`

```lua
character:move(0, true)
```
Moves the `character` one step in the `direction`, is the movement performed
actively `activeMove` should be `true` otherwise `false`.

#### `turn(number direction)`
#### `turn(posStruct position)`

```lua
character:turn(0)
character:turn(position(1,1,0))
```
Turns the character either towards a `direction` or towards a `position`.

#### `warp(posStruct position)`
#### `forceWarp(posStruct position)`
```lua
character:warp(position(1,1,1))
character:forceWarp(position(1,1,1))
```
Warps the character to a certain `position`. While warp(position)
is going to protect the character to be spawned on a non-moveable position,
forceWarp ignores this aspect.

#### `isInRage(character secondCharacter, number distance)``
```lua
character:isInRage(secondCharacter, 5)
```
Returns `true` if `secondCharacter` is within `distance` of the character, else `false`.

#### `isInRangeToPosition(posStruct position, number distance)`

Returns `true` if the character is within the `distance` of `position`, else `false`.

#### `distanceMetric(character secondCharacter)`
#### `distanceMetricToPosition(posStruct position)`
```lua
character:distanceMetric(secondCharacter)
character:distanceMetricToPosition(position(1,1,1))
```

Returns distance between the character and a `secondCharacter`
or between the character and a `position`.
