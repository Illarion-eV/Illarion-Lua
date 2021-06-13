### Attributes

* General Information

#### `getPlayerLanguage()`
```lua
character:getPlayerLanguage()
```
Returns the player’s language: Player.german or Player.english.

#### `boolean isNewPlayer()`
```lua
character:isNewPlayer()
```
Returns whether character is a new player or not.

#### `boolean isAdmin()`
```lua
character:isAdmin()
```
Returns true if that character is admin (GM) and false otherwise.

#### `number idleTime()`
```lua
character:idleTime()
```
If the character is a player, returns the number of seconds they are idle. Returns 0 otherwise.

#### `boolean isValidChar(character Char)`
```lua
isValidChar(char)
```
Returns true if `char` is still valid and safe to use. Validity has to be checked if char is
used in another entrypoint call than the one where it was originally obtained, since a player
might have logged out, an NPC might have been deleted and a monster might have been
killed in the meantime.

#### `number getMonsterType()`
```lua
character:getMonsterType()
```
Returns the monster-ID of a monster.

#### `number getType()`
```lua
character:getType()
```
Returns Character.player for players, Character.monster for monsters and Character.npc for
NPCs.

* Appearance

Setters

#### `setSkinColour(colour skinColour)`
```lua
character:setSkinColour(colour(0,0,0))
```
Sets the skin colour.

#### `setHairColour(colour hariColour)`
```lua
character:setHairColour(colour(255,255,255))
```
Sets hair and beard colour.

#### `setHair(number hairID)`
```lua
character:setHair(1)
```
Changes the character hair to given one.

#### `setBeard(number beardID)`
```lua
character:setBeard(3)
```
Changes the beard of the character to the given one.

#### `setRace(number race)`
```lua
character:setRace(4)
```
Temporarily sets the race of a character.

Getters

#### `colour getSkinColour()`
```lua
character:getSkinColour()
```
Returns skin colour.

#### `colour getHairColour()`
```lua
character:getHairColour()
```
Returns hair color.

#### `number getHair()`
```lua
character:getHair()
```
Returns the ID of the present hair, 0 for no hair.

#### `number getBeard()`
```lua
character:getBeard()
```
Returns the ID of the present beard, 0 for no beard.

#### `number getRace()`
```lua
character:getRace()
```
Returns the race of a character.

* Constitution

#### `increasePoisonValue(number amount)`
```lua
character:increasePoisonValue(5)
```
Increases the toxication with the given `amount`.

#### `number getPoisonValue()`
```lua
character:getPoisonValue()
```
Returns the character's toxication value.

#### `setPoisonValue(number value)`
```lua
character:setPoisonValue(100)
```
Sets the toxication to the given `value`.

#### `number getMentalCapacity()`
```lua
character:getMentalCapacity()
```
Returns the mental capacity of the character which influences the ability to skill.

#### `setMentalCapacity(number value)`
```lua
character:setMentalCapacity(100)
```
Sets the mental capacity of the character to the given `value`

#### `increaseMentalCapacity(number amount)`
```lua
character:increaseMentalCapacity(20)
```
Increases the mental capacity of the character with the given `amount`.

* Modifying attributes

#### `number increaseAttrib(string attribute, number value)`
```lua
character:increaseAttrib("intelligence",100)
```
Increases the attribute given (see below) and returns the new attribute `value`. Use `value`=0
to read the attribute’s value. Note that this command also sends a player update to all characters in range if necessary.

#### `setAttrib(string attribute, number value)`
```lua
character:setAttrib("hitpoints", 1)
```
Sets the given `value` for the given `attribute`.
Be aware that any attribute change to fixed attributes like "strength" will only last for the
current session and will be reset to the database value upon the next login.

#### `boolean isBaseAttributeValid(string attribute, number value)`
```lua
character:isBaseAttributeValid("strength",0)
```
Returns whether `value` is acceptable for the given `attribute` and the race of the character,
respecting limits given in table.

#### `number getBaseAttributeSum()`
```lua
character:getBaseAttributeSum()
```
Returns the current sum of the eight primary attributes.

#### `number getMaxAttributePoints()`
```lua
character:getMaxAttributePoints()
```
Returns the maximum value which the sum of primary attributes should have.

#### `number getBaseAttribute(string attribute)`
Returns the base value of the given `attribute`, that is the value that this attribute normally
has, when no special effects are active.

#### `boolean setBaseAttribute(string attribute, number value)``
Sets the base value of the given `attribute` and returns `true` if isBaseAttributeValid(...)
would return `true`. Otherwise is a no-op and returns `false`.

#### `boolean increaseBaseAttribute(string attribute, number amount)`
```lua
character:increaseBaseAttribute("strength",20)
```
If isBaseAttributeValid(...) would return `true`, increases or decreases the base value of
the given `attribute` and returns `true`. Otherwise is a no-op and returns `false`.

#### `boolean saveBaseAttributes()`
```lua
character:saveBaseAttributes()
```
Saves the eight primary base attributes to the database, iff getBaseAttributeSum() ==
getMaxAttributePoints(). On failure resets primary attribute values to database values.
Returns whether the operation was successful or not.


* Magic

Illarion distinguishes between four magic types: Mages(0), Priests(1), Bards(2) and Druids(3).

#### `number getMagicType()`
```lua
character:getMagicType()
```
Returns the magic type of the character.

#### `setMagicType(number magicType)`

```lua
-- Be a druid
character:setMagicType(3)
```
Changes the magic type of the character to the given `magicType`.

#### `number getMagicFlags(number magicType)`

```lua
character:getMagicFlags(0)
```
Returns the number of magicFlags of the given `magicType`.

#### `teachMagic(number magicType,number magicFlag)`

```lua
-- Teach rune with ID 1
character:teachMagic(0,2^(1))
```
Can be used to teach a character runes or other flags, based on the given `magicType`and `magicFlag`.
