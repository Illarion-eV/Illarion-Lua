## Long Time Effect

Stored in a character's `effects` variable. See section "Long Time Effects" for [Character](#character) on how to access
it. For a description on how to use long time effects, see their [entry point](#long-time-effects) section.

### Variables

Name         | Type   | Writable | Description
------------ | ------ | -------- | -----------
effectId     | number | no       | effect id
effectName   | string | no       | effect name 
nextCalled   | number | yes      | number of deciseconds until the effect should be called
numberCalled | number | no       | number of times the effect has been called before, meaning on the first call this will be zero, etc.

### Functions

```lua
local effect = LongTimeEffect(10, 50)
effect:addValue("totalCalls", 10)
local exists, value = effect:findValue("totalCalls")

if exists then
    effect:addValue("totalCalls", value + 10)
else
    effect:addValue("totalCalls", 10)
end

effect:removeValue("totalCalls")
```

#### `LongTimeEffect(number id, number nextCalled)`

Returns a new LongTimeEffect with given `id` and `nextCalled` being the number of deciseconds until the effect is first
called via entry point `callEffect` after being added to a character.

#### `addValue(string key, number value)`

Adds or overwrites variable `key` with value `value`. `value` is non-negative and less than 2^32.

#### `boolean, number findValue(string key)`

Returns false if the effect has no variable with name `key`. Otherwise returns `true` and the value of that variable.

#### `removeValue(string key)`

Removes variable with name `key` from the effect.