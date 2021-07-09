## Learning

> Learning script with all available entry points

```lua
local M = {}

function M.learn(user, skill, actionPoints, learnLimit)
end

function M.reduceMC(user)
end

return M
```

**Script file:** `server/learn.lua`

### `learn(Character user, number skill, number actionPoints, number learnLimit)`

Called as a result of `user:learn` being invoked. `skill` IDs are defined in the database table `skills`. A certain
number of `actionPoints` were spent on an action, resulting in learning. The learned skill cannot exceed both
`learnLimit` and `100`.

### `reduceMC(Character user)`

Called every 10s for every online player. Use this to reduce mental capacity with `user:increaseMentalCapacity`. A 
higher mental capacity value makes learning more difficult.