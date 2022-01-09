## Talk

> Talk script with all available entry points

```lua
local M = {}

function M.talk(user, talkType, text)
    return text
end

return M
```

**Script file:** `server/playertalk.lua`

### `boolean actionDisturbed(Character user, Character attacker)`
Is called when `user` is attacked while an action is running. This action had to be started by `user:startAction(...)`
in `talk`. If this entry point does not exist or returns `false` the action is not aborted. If it returns `true` the
action is aborted. See section Actions in [Character](#character) for more details on starting actions.

### `string talk(Character user, number talkType, string text, number actionState)`

Is called when player `user` tries to speak `text`. `talkType` is one of `Character.say`, `Character.whisper`
and `Character.yell`. Needs to return the text the player will actually speak.

This can be used for speaking passwords, reciting spells, making players sound drunk, etc.

`actionState` is one of

* `Action.none`: no action is running.
* `Action.success`: an action was running and has been completed.
* `Action.abort`: an action was running and has been interrupted by the user being attacked or the user doing something
else like using an item, moving, etc.

See section Actions in [Character](#character) for more details on starting actions.