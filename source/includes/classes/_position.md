## position

Positions represent a location on the world map.

### Variables

Name | Type   | Writable  | Description
---- | ------ | --------- | -----------
x    | number | yes       | x coordinate, increases from west to east (lower left to upper right)
y    | number | yes       | y coordinate, increases from north to south (upper left to lower right)
z    | number | yes       | z coordinate, increases as levels go up

### Functions

#### `position(number x, number y, number z)`
```lua
local pos = position(10, 11, 0)
```
Returns position for map location (x, y, z).

#### `position p1 == position p2`
```lua
local equal = position(4, 5, 0) == position(4, 5, 0) -- equal == true
```
Compares two positions `p1` and `p2`. Returns

* `true` if `p1.x == p2.x and p1.y == p2.y and p1.z == p2.z`
* `false` otherwise

### Free Functions

#### `tostring(position p)`
```lua
local text = tostring(position(3, 4, 0)) -- text == "(3, 4, 0)"
```
Returns `"(" .. p.x .. ", " .. p.y .. ", " .. p.z .. ")"`.

<aside class="warning">
A position obtained from a character is still linked to that character and will change when the character moves.
</aside>

```lua
user:forceWarp(position(0, 0, 0))
local pos = user.pos              -- pos is (0, 0, 0)
user:forceWarp(position(1, 1, 0)) -- now user.pos AND pos are (1, 1, 0)
```
> Avoid this by creating a new position from individual coordinates.

```lua
local pos = position(user.pos.x, user.pos.y, user.pos.z)
```

