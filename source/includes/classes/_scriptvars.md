## Script Variables

`ScriptVars` is a global variable, allowing us to save values in the database and to access them with an identifier
string. Use with caution as these values have global effect. Everything in `ScriptVars` is automatically saved upon
server shutdown.

### Functions

```lua
ScriptVars:set("welcome", "Welcome to Illarion")
local found, message = ScriptVars:find("welcome")
ScriptVars:remove("something")
ScriptVars:save()

```

#### `boolean, string find(string key)`

Returns `false` if a ScriptVar `key` does not exist. Otherwise returns `true` and the value of ScriptVar `key`.

#### `boolean remove(string key)`

Removes ScriptVar `key` and returns `true` if there was such an entry. Returns `false` otherwise.

#### `save()`

Saves all ScriptVars immediately. Use with caution, this might cause lag.

#### `set(string key, number value)`
#### `set(string key, string value)`

Writes `value` into ScriptVar `key`. Values are always stored as strings.