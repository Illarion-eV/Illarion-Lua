## NPCs
```lua
local M = {}

function M.nextCycle (npc)
end

function M.receiveText(npc)
end
function M.useNPC(npc, user)
    -- What should happen when you use the npc
end
lookAtNpc(npc, player, mode)
    -- The lookat for the npc (Not in use? Found no existing examples)
return M
```

NPC entry points are only run when a player is within a range of 60 fields, two levels up and down,
or if the NPC is on a route.

### `lookAtNpc(npc, user, mode)`
Invoked when `user` looks at `npc` with `mode` being one of:

* `Player.look`: casual inspection
* `Player.stare`: thorough inspection

<aside class="info">
The current client does not support Player.look, so mode will always be Player.stare
</aside>

### `nextCycle(npc)`
    Invoked every decisecond if a player is nearby or `npc` is on a route.

### `receiveText(npc, talkType, message, talker)`
    Invoked anytime the NPC hears someone speaking.

### `useNPC(npc, user, actionState)`
    Invoked when the user shift clicks the NPC.
