## Fields

These entry points are bound to a single field (x, y, z) on the map.

> SQL

```sql
INSERT INTO triggerfields VALUES (X, Y, Z, 'SCRIPT_NAME');
```

> Field script with all available entry points

```lua
local M = {}

function M.ItemRotsOnField(oldItem, newItem)
end

function M.MoveFromField(user)
end

function M.MoveToField(user)
end

function M.PutItemOnField(item, user)
end

function M.TakeItemFromField(item, user)
end

return M
```

**Database table:** `triggerfields`

### `ItemRotsOnField(Item oldItem, Item newItem)`

<aside class="info">
Currently the server does not call ItemRotsOnField.
</aside>

`oldItem` had its wear reduced to zero on this field and rots into `newItem`.

### `MoveFromField(Character user)`

`user` moves away from this field.

### `MoveToField(Character user)`

`user` moves onto this field.

### `PutItemOnField(Item item, Character user)`

`user` puts `item` on this field.

### `TakeItemFromField(Item item, Character user)`

`user` takes `item` from this field.