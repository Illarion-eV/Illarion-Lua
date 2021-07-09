## Quests
```lua
local common = require("base.common")
local M = {}

function M.QuestTitle(user)
    return common.GetNLS(user, "German title text here", "English title text here")
end

function M.QuestDescription(user, status)

    local german = -- German description text here
    local english = -- English description text here

    return common.GetNLS(user, german, english)
end

local QuestTarget = {}
QuestTarget[1] = {position(x, y, z) -- replace x, y, z with desired coordinates
QuestTarget[2] = {position(x, y, z)

function M.QuestTargets(user, status)
    return QuestTarget[status]
end

function M.QuestFinalStatus()
    return 3 -- Change this number according to what the final quest status is.
end

return M
```
While you can create quests with setQuestProgress and getQuestProgress, it is much nicer to have an
actual log of that progress in your client. This way you cannot forget about your quests and you always
know what to do and where to do it. The client might even point you in the right direction. The entrypoints in this section implement that behaviour.

**function QuestTitle(user)**

You should return the quest title here, depending on user language.

**function QuestDescription(user, status)**

You should return the quest description here, depending on user language and quest status.
You can be as extensive as you want, but make sure to cover the most important points. A
good description should serve as a reminder where to go to complete the next step of the
quest, let the player know how to get there and what to do there. Imagine a player continuing
a quest after some time, they still need to know where they are at and how to go on.


**function QuestTargets(user, status)**

Here you should return the position where the quest continues, i.e. where a new quest status
can be obtained. The client will receive this position and direct the player towards it. You
can also return nil or an empty list if no such positions should be displayed in the client.
Omit positions with care. Even if you think it would be cool to let players search on their
own, most of the time it is just annoying. You can also return a list of positions here if the
quest can continue in more than one location.

**function QuestFinalStatus()**

Return the final status of your quest here. This is used by the server to determine whether the
end of a quest has been reached. If so, the client is notified to display the quest as completed

**Database Table:**`quests`

Quest scripts must be entered into the database for the functions to be applied to the associated quest.

|qst_id|qst_script|
|------|----------|
|603|quest.nobarg_603|

The example above is for a quest associated with the npc nobarg, with the quest id 603.

In the qst_id entry is the id assigned to the quest.

In the qest_script entry is the folder the script is in (quest) and the name of the .lua file (nobarg_603).