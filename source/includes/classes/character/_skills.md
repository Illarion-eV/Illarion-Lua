### Skills

#### `getSkillName(skill targetSkill)`

```lua
character:getSkillName(Character.ancientLanguage)
```
Returns the name of the given `skill` in the player’s language.

#### `getSkill(skill targetSkill)``
```lua
character:getSkill(Character.ancientLanguage)
```

Returns the major `skill` value for the character.
#### `getSkillValue(skill targetSkill)``

```lua
character:getSkillValue(Character.ancientLanguage)
```

Returns a table with two fields, major and minor, representing the `skill` and the minor skill.

#### `setSkill(skill targetSkill, number major, number minor)``
```lua
character:setSkill(Character.ancientLanguage, 15, 10)
```
Directly sets major and minor skill. Returns the new major skill. If the skill does not exist in the database, nothing is set and 0 is returned.

#### `increaseSkill(skill targetSkill, number value)`
#### `increaseMinorSkill(skill targetSkill, number value)`
```lua
character:increaseSkill(Character.ancientLanguage, 10)
character:increaseMinorSkill(Character.slashingWeapons, 10)
```
Increase major and minor skill, respectively. Returns the new major skill. If the skill does not exist in the database, nothing is increased and 0 is returned.

#### `learn(skill targetSkill, number actionPoints, number learnLimit)`
```lua
character:learn(Character.slashingWeapons, 10,100)
```
Number of `actionPoints` used up for the action which resulted in learning, but the skill will not be advanced beyond this `learnLimit` and never beyond 100.
