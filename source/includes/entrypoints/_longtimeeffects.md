## Long Time Effects

[Long time effects](#long-time-effect) (LTE) allow you to influence a character over a period of time. Their state is
saved whenever the character is saved. They consist of:

* ID and name 
* a script defining the LTE
* a counter tracking how often an effect had been called already
* a variable controlling when the effect will be called again
* several user-defined variables accessible by a key string and holding integers

After adding an LTE to the database, you can add it to a character, e.g. inside an item script. How the effect works has
to be defined in its script. Every time the LTE is called, the entry point `callEffect` is invoked. There you can change
the character's attributes etc. Note that you should always save any changes of fixed attributes in LTE variables, so
you can restore everything when the LTE ends. When a character logs out, all its variables are saved. When it logs in
again, the `loadEffect` is invoked. Any temporary changes of attributes will be lost on logout, so here you can read
the values you have saved and perform the changes again.

> SQL

```sql
INSERT INTO longtimeeffects VALUES (ID, 'EFFECT_NAME', 'SCRIPT_NAME');
```

> LTE script with all available entry points

```lua
local M = {}

function M.addEffect(effect, user)
    user:inform("added " .. effect.effectName)
end

function M.callEffect(effect, user)
    user:inform("called " .. effect.effectName .. ", next: " .. effect.nextCalled .. ", called before: " .. effect.numberCalled)
    return true
end

function M.doubleEffect(effect, user)
    user:inform("doubled " .. effect.effectName)
end

function M.loadEffect(effect, user)
    user:inform("loaded " .. effect.effectName)
end

function M.removeEffect(effect, user)
    user:inform("removed " .. effect.effectName)
end

return M
```

**Database table:** `longtimeeffects`

### `addEffect(LongTimeEffect effect, Character user)`

A new `effect` has been added to `user`.

### `bool callEffect(LongTimeEffect effect, Character user)`

An `effect` activates for `user`. If `true` is returned, the effect will be called again in `effect.nextCalled`
deciseconds. If `false` is returned, the effect will be removed.

### `doubleEffect(LongTimeEffect effect, Character user)`

A script tried to add an effect to `user`, but `effect` which has the same id, was already present. This can be used
e.g. to refresh the overall duration of `effect`, by modifying a variable which stores the number of
times the effect needs to be called.

### `loadEffect(LongTimeEffect effect, Character user)`

A `user` has logged into the game afflicted by `effect`. Temporary changes need to be recreated here.

### `removeEffect(LongTimeEffect effect, Character user)`

An `effect` was removed from `user` either by returning `false` in `callEffect` or by calling
`user.effects:removeEffect(id)`.