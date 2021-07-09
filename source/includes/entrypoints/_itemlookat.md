## Item Inspection

> Item inspection script with all available entry points

```lua
local M = {}

function M.lookAtItem(user, item)
    local lookAt = ItemLookAt()
    return lookAt
end

return M
```

**Script file:** `server/itemlookat.lua`

### `ItemLookAt lookAtItem(Character user, Item item)`

Handles basic item inspection if `item` does not have a script with `LookAtItem` entry point. Needs to return an
[ItemLookAt](#itemlookat).