## Combat

> Combat script with all available entry points

```lua
local M = {}

function M.onAttack(attacker, defender)
end

return M
```

**Script file:** `server/standardfighting.lua`

### `onAttack(Character attacker, Character defender)`

Is called every time `attacker` tries to hit `defender` in physical combat.