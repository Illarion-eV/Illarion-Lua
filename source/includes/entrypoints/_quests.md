## Quests

```sql
INSERT INTO quests VALUES (QUEST_ID, 'QUEST_SCRIPT');
```

```lua
local common = require("base.common")
local M = {}

local GERMAN = Player.german
local ENGLISH = Player.english

local title = {}
title[GERMAN] = "Deutscher Questtitel"
title[ENGLISH] = "English Quest Title"

local description = {}
description[GERMAN] = {}
description[ENGLISH] = {}
description[GERMAN][1] = "Tolle lange Beschreibung die angezeigt wird wenn man Queststatus 1 erreicht, \z
                          auch was man wo machen muss ..."
description[ENGLISH][1] = "Cool long description which is displayed when you reach quest status 1, \z
                           also mention what to do where ..."

local start = position(1, 2, 3)

local questTarget = {}
questTarget[1] = {position(1, 2, 3), position(4, 5, 6)}

local FINAL_QUEST_STATUS = 0

function M.QuestTitle(user)
    return common.GetNLS(user, title[GERMAN], title[ENGLISH])
end

function M.QuestDescription(user, status)
    local german = description[GERMAN][status] or ""
    local english = description[ENGLISH][status] or ""

    return common.GetNLS(user, german, english)
end

function M.QuestAvailability(user, status)
    if status == 0 then
        return Player.questAvailable
    else
        return Player.questNotAvailable
    end
end

function M.QuestStart()
    return start
end

function M.QuestTargets(user, status)
    return questTarget[status]
end

function M.QuestFinalStatus()
    return FINAL_QUEST_STATUS
end

return M
```

> A more extensive template is available in `quest/quest.template`

While you can create quests with `setQuestProgress` and `getQuestProgress` alone, it is nice to have an actual
log of your quest progress in your client. This way you cannot forget about your quests and you always
know what to do and where to do it. The client might even point you in the right direction. The entrypoints in this
section implement that behaviour.

**Database Table:** `quests`

Quest scripts must be entered into the database for the functions to be applied to the associated quest.

|qst_id|qst_script|
|------|----------|
|603|quest.nobarg_603|

The example above is for a quest associated with the npc nobarg, with the quest id 603. In the `qst_id` entry is the id
assigned to the quest. In the `qst_script` entry is the folder the script is in (quest) and the name of the .lua file
(nobarg_603).

### `string QuestTitle(Character user)`

You should return the quest title here, depending on user language.

### `string QuestDescription(Character user, number status)`

You should return the quest description here, depending on user language and quest status.
You can be as extensive as you want, but make sure to cover the most important points. A
good description should serve as a reminder where to go to complete the next step of the
quest. Let the player know how to get there and what to do there. Imagine a player continuing
a quest after some time, they still need to know where they are at and how to go on.

### `position QuestStart()`

Return the position where the quest begins. This will probably be the position of an NPC or item.

### `number QuestAvailability(Character user, number status)`

You can return three possible values here, depending on the `user` and the current quest `status`:

* `Player.questAvailable`: yellow quest marker "!"
* `Player.questWillBeAvailable`: grey quest marker "!"
* `Player.questNotAvailable`: no quest marker

If the quest could be available soon (e.g. missing skill) return `Player.questWillBeAvailable`
and if the player tries to accept the quest, inform them what exactly is missing to do so.
If the quest will not be available (wrong town, too much skill already, etc.) return
`Player.questNotAvailable`.

If this entry point is not defined, the server will assume `Player.questAvailable` for `status == 0`
and `Player.questNotAvailable` otherwise.

### `list|position QuestTargets(Character user, number status)`

Here you should return the position where the quest continues, i.e. where a new quest status
can be obtained. The client will receive this position and direct the player towards it. You
can also return nil or an empty list if no such positions should be displayed in the client.
Omit positions with care. Even if you think it would be cool to let players search on their
own, most of the time it is just annoying. You can also return a list of positions here if the
quest can continue in more than one location.

### `number QuestFinalStatus()`

Return the final status of your quest here. This is used by the server to determine whether the
end of a quest has been reached. If so, the client is notified to display the quest as completed.