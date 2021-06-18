## Magic

**function CastMagic(caster)**

```lua
local M = {}
function M.CastMagic(user)
    -- The spell effect?
end
return M
```

Invoked when the caster casts a spell without a target.

**function CastMagicOnCharacter(caster, targetCharacter)**

```lua
local M = {}
function M.CastMagicOnCharacter(user, target)
    -- The spell effect?
end
return M
```

Invoked when the caster casts a spell on a targeteted character/monster.

**function CastMagicOnField(caster, targetPosition)**

```lua
local M = {}
function M.CastMagicOnField(user, target)
    -- The spell effect?
end
return M
```

Invoked when caster casts a spell on a field at the specified position.

**function CastMagicOnItem(caster, targetItem)**

```lua
local M = {}
function M.CastMagicOnItem(user, target)
    -- The spell effect?
end
return M
```

Invoked when a spell is cast on a targeted item.