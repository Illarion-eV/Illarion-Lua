## Logout

> Logout script with all available entry points

```lua
local M = {}

function M.onLogout(user)
end

return M
```

**Script file:** `server/logout.lua`

### `onLogout(Character user)`

Invoked when `user` logs out. Here you can e.g. substitute player faction leaders with their NPC equivalent.