## Death

> Death script with all available entry points

```lua
local M = {}

function M.playerDeath(user)
end

return M
```

**Script file:** `server/playerdeath.lua`

### `playerDeath(Character user)`

Is called when `user` dies. Here you can handle e.g. penalties for dying.