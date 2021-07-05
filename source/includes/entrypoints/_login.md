## Login

> Login script with all available entry points

```lua
local M = {}

function M.onLogin(user)
end

return M
```

**Script file:** `server/login.lua`

### `onLogin(Character user)`

Invoked when `user` logs in. Here you can display login information, tax players, etc.