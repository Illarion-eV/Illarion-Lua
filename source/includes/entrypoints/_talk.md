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

### `string talk(Character user, number talkType, string text)`

Is called when player `user` tries to speak `text`. `talkType` is one of `Character.say`, `Character.whisper`
and `Character.yell`. Needs to return the text the player will actually speak.

This can be used for speaking passwords, reciting spells, making players sound drunk, etc.