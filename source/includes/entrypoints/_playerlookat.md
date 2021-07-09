## Player Inspection

> Player inspection script with all available entry points

```lua
local M = {}

function M.lookAtPlayer(user, targetPlayer, mode)
end

return M
```

**Script file:** `server/playerlookat.lua`

### `lookAtPlayer(Character user, Character targetPlayer, number mode)`

Is invoked when `user` looks at `targetPlayer`. For normal inspection `mode` is 0, for close examination `mode` is 1.