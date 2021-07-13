### Character - Attack
#### `callAttackScript(character attacker, character defender)`
```lua
character:callAttackScript(character, defender)
```
Calls the `onAttack` function of the right hand item of the `attacker`
against the `defender`.

#### `boolean attackmode()`
```lua
character:attackmode()
```
Returns `true`if the current character is attacking.

#### `stopAttack()`
```lua
character:stopAttack()
```
Stops the attack.
#### `character getAttackTarget()`
```lua
character:getAttackTarget()
```
Returns the attack target of the current character.
