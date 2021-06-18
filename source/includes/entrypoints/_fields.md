## Fields
**function useTile(user, position)**

```lua
local M = {}
function M.useTile(user, position)
    -- What should happen if you use the tile on the triggerfield.
end
return M
```

    Is invoked when a tile is shift-clicked (used).

**function PutItemOnField(item, user)**

```lua
local M = {}
function M.putItemOnField(item, user)
    -- What should happen if the item is put on the triggerfield.
end
return M
```

    Is invoked if an item is put on that triggerfield.

**function TakeItemFromField(item, user)**

```lua
local M = {}
function M.TakeItemFromField(item, user)
    -- What should happen if you remove an item from the triggerfield.
end
return M
```

    Is invoked if an item is taken away from that triggerfield.

**function ItemRotsOnField(oldItem,newItem)**

```lua
local M = {}
function M.ItemRotsOnField(176, 178)
-- Turns grey cloth into white cloth upon rotting if placed on the triggerfield.
return M
```

    Is invoked when an item on a triggerfield rots, turning the oldItem into the newItem.

**function MoveToField(user)**

```lua
local M = {}
function M.MoveToField(user)
    -- What should happen if a character steps onto the triggerfield.
end
return M
```

    Is invoked if a character moves on that triggerfield.

**function MoveFromField(user)**

```lua
local M = {}
function M.MoveFromField(user)
    -- What should happen if a character leaves the triggerfield.
end
return M
```

    Is invoked if a character moves away from that triggerfield.


**Database Table:**`triggerfields`

Entry in the database is required for any of the above functions to work on the specified tile.

|tgf_posx|tgf_posy|tgf_posz|tgf_script|
|--------|--------|--------|----------|
|x|y|z|triggerfield.myScript|

**Positions**

The first three database entries for triggerfields consist of the x, y, z coordinates that define your field.

**Script Name**

The fourth and last database entry for triggerfields is the name of your script. In this case the "myScript.lua" found in the folder "triggerfield".



