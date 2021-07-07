## Character

Players, NPCs and monsters are the three types of characters in Illarion.

![directions](images/directions.png)

### Variables

Name           | Type     | Writable  | Description
-------------- | -------- | --------- | -----------
id             | number   | no        | character id
effects        | userdata | no        | contains methods to control the character's long time effects, see section on long time effects.
name           | text     | no        | character name
pos            | position | no        | character position on world map
lastSpokenText | text     | no        | character's last spoken line of text
attackmode     | boolean  | no        | `true` if character currently attacks, `false` otherwise
activeLanguage | number   | yes       | 0: common, 1: human, 2: dwarf, 3: elf, 4: lizard, 5: orc, 6: halfling, 7: fairy, 8: gnome, 9: goblin, 10: ancient
movepoints     | number   | yes       | A character has a maximum of 21 movepoints. Every action like talking, fighting, using etc. needs at least 7 movepoints. The reduction of movepoints depends on the character's agility. A character gains one movepoint per decisecond.

### Actions

```lua
local M = {}

function M.UseItem(user, item, actionState)
    local gfxRain = 16

    if actionState == Action.none then
        user:startAction(50, gfxRain, 20, 0, 0)
        user:inform("start")
        item.number = item.number + 1
        world:changeItem(item)
        user:changeSource(item)
    elseif actionState == Action.abort then
        user:inform("abort: " .. item.number)
    elseif actionState == Action.success then
        user:inform("success: " .. item.number)
    end
end

function M.actionDisturbed(user, attacker)
    user:inform("disturbed by " .. attacker.name)
    return true
end

return M
```

All Use* entry points (e.g. UseItem) which have an `actionState` parameter, allow for starting actions. An action can be
seen as a state of concentration of the user, which lasts for a specified time. After that time or when the action is
interrupted, the entry point is called again with the same parameters, but with actionState set to `Action.abort` or
`Action.success` accordingly. Usually actions are aborted by the user doing something else, like using something,
moving, etc. However, actions can also be aborted by the user being attacked if an `actionDisturbed` entry point is
defined and returns `true`.

#### `startAction(number duration, number gfxId, number gfxInterval, number sfxId, number sfxInterval)`

Starts an action lasting `duration` deciseconds. At the start of the action and every `gfxInterval` deciseconds after
that [graphic effect](https://illarion.org/~devserver/effects/effects.html) `gfxId` is played.
Similarly, at the start of the action and every `sfxInterval` deciseconds after
that [sound effect](https://illarion.org/~devserver/sounds/sounds.html) `sfxId` is played. If `gfxId` or `sfxId` are set
to `0`, no effect of that type will be played.

#### `changeSource(Item item)`
If you modify the `item` associated with an action started in `UseItem`, this functions ensures the next time
`UseItem` is called by the action (when it succeeds or is aborted) the updated item will be provided as a parameter.
This needs to be called in addition to `world:changeItem`.

### Long Time Effects

See class [LongTimeEffect](#long-time-effect) for details.

#### `effects:addEffect(LongTimeEffect effect)`

```lua
local effect = LongTimeEffect(10, 50)
user.effects:addEffect(effect)
```

Tries to add `effect` to the character. [Entry point](#long-time-effects) `addEffect` is called immediately if the
effect is not yet present on the character. Otherwise entry point `doubleEffect` is called.

#### `boolean, LongTimeEffect effects.find(number id)`
#### `boolean, LongTimeEffect effects.find(string name)`

```lua
local found, effect = user.effects:find("some effect")
```

Searches for a long time effect by `id` or `name` and returns `true` and that effect if it exists on this character.
Returns `false` if that effect does not exist on this character.

#### `boolean effects:removeEffect(number id)`
#### `boolean effects:removeEffect(string name)`
#### `boolean effects:removeEffect(LongTimeEffect effect)`

```lua
local removed = user.effects:removeEffect(10)
```

Removes an effect from this character, either by `id`, by `name` or by passing the `effect` itself. Returns `true` if an
effect was removed and `false` otherwise.

### Text/Speech Functions

#### `talk(number mode, text message)`
```lua
user:talk(Character.say, "Hello World!")
```
Lets a character say/whisper/yell a `message`. `mode` can be `Character.say`, `Character.whisper` or `Character.yell`.

