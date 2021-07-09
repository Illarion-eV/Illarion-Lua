## Depot

> Depot script with all available entry points

```lua
local M = {}

function M.onOpenDepot(user, depot)
    return true
end

return M
```

**Script file:** `server/depot.lua`

### `boolean onOpenDepot(Character user, Item depot)`

Is called when `user` tries to open a `depot`. Has to return `true` if `user` is allowed to open this `depot` and
`false` otherwise.