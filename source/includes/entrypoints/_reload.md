## Reloading Scripts

> Reload script with all available entry points

```lua
local M = {}

function M.onReload()
    return true
end

return M
```

**Script file:** `server/reload.lua`

### `boolean onReload()`

Invoked after server start as well as after the `!fr` command has been issued in the client. Needs to return `true` for
the reload to succeed. If `false` is returned, the reload will fail. You can use this for initialising code that would
otherwise not run on reload.

Most of the time any initialisation should be performed in a related script, though. The server will run all scripts
entered into the database as well as all server scripts on every reload and server start. Keep in mind that you _can_
put code in a file outside of any function and it will be run at those times.