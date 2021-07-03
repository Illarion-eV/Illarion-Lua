## Items

> SQL

```sql
UPDATE items SET itm_script = 'SCRIPT_NAME' WHERE itm_id = ITEM_ID;
```

> Item script with all available entry points

```lua
local M = {}

function M.actionDisturbed(user, disturber)
    return false
end

function M.CharacterOnField(user)
end

function M.LookAtItem(user, item)
    local lookAt = ItemLookAt()
    return lookAt
end

function M.MoveItemAfterMove(user, source, target)
end

function M.MoveItemBeforeMove(user, source, target)
    return true
end

function M.UseItem(user, item, actionState)
end

return M
```

**Database field:** `items.itm_script`

### `boolean actionDisturbed(Character user, Character attacker)`
Is called when `user` is attacked while an action is running. This action had to be started by `user:startAction(...)`
in `UseItem`. If this entry point does not exist or returns `false` the action is not aborted. If it returns `true` the
action is aborted. See section Actions in [Character](#character) for more details on starting actions.

### `CharacterOnField(Character user)`
Is invoked if someone steps on an item. For this entry point to be called, the corresponding
item needs to have an entry in the database table tilesmodificators with tim_specialitem set to `true`.

### `ItemLookAt LookAtItem(Character user, Item item)`
A `user` looks at an `item`. Needs to return an [ItemLookAt](#itemlookat).

### `boolean MoveItemBeforeMove(Character user, Item source, Item target)`
A `user` tries to move the item `source`. After the move that item would be `target`, having a new location.
If this returns `true` or if this entry point does not exist, the move is carried out. If `false` is returned, the move
is prevented.

### `MoveItemAfterMove(Character user, Item source, Item target)`
A `user` has moved the item `source`. It is now the item `target`.

### `UseItem(Character user, Item item, number actionState)`

A `user` uses an `item`. `actionState` is one of

* `Action.none`: no action is running.
* `Action.success`: an action was running and has been completed.
* `Action.abort`: an action was running and has been interrupted by the user being attacked or the user doing something
else like using an item, moving, etc.

See section Actions in [Character](#character) for more details on starting actions.