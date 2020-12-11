## colour

Colours are used to represent a characters skin or hair colour.

### Variables

Name  | Type   | Writable  | Description
----- | ------ | --------- | -----------
red   | number | yes       | From 0 (no red) to 255 (full red)
green | number | yes       | From 0 (no green) to 255 (full green)
blue  | number | yes       | From 0 (no blue) to 255 (full blue)
alpha | number | yes       | From 0 (transparent) to 255 (opaque)

### Functions

#### `colour(number red, number green, number blue [, number alpha = 255])`
```lua
local black = colour(0, 0, 0)
```
Creates colour for given RGBA values.

