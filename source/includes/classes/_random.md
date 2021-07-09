## Random

Most of the time the random number generator supplied by Lua should be enough. However, if you are looking for a
statistically sound implementation of a random number generator, or if you need another distribution besides the uniform
one, this is the class you are looking for.

### Functions

These functions belong to the class `Random` and not to variables of type `Random`. As such they use the `.` delimeter
instead of `:`. It is not possible to create variables of type `Random`.

#### `number uniform()`

```lua
local chance = Random.uniform()
```

Returns a random floating-point value uniformly distributed in the range [0, 1).

#### `number uniform(number min, number max)`

```lua
local die = Random.uniform(1, 6)
```

Returns a random integer value uniformly distributed in the integer range [`min`, `max`]

#### `number normal(number mean, number standard_deviation)`

```lua
local chance = Random.normal(10.75, 1.2)
```

Returns a random floating-point value normally distributed with given `mean`and `standard_deviation`.