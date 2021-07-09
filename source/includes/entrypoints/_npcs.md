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

nextCycle (npc)
    Invoked every few server cycles.
    Must exist in NPC scripts.
receiveText(npc)
    Invoked anytime the NPC hears someone speaking.
useNPC(npc, user)
    Invoked when the user shift clicks the NPC.
lookAtNpc(npc, player, mode)
    Invoked if the player looks at the NPC.
    Modes: 0 for normal, 1 for close examination.