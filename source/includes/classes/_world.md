## world

### Functions

```lua

local myPosition = position(134, 348, 0)

local myField = world:getField(myPosition)

local tileID = myField.tile

```

#### `field world:getField(posStruct position)`

Returns a reference to the field that is on the given position.
Used to get information such as the ID of the tile that is on the field, or other functionality listed in the entry for the field class further up on the page.


```lua

local function compareOldTimeWithNewTime(oldTime)

    local time = world:getTime("unix")

    local timeThatHasPassedInSeconds = time-oldTime

    return timeThatHasPassedInSeconds

end


```

#### `number world:getTime(text time)`

Fetches the time, depending on the input, which can be the following: "year", "month", "day", "hour", "minute", "second", "unix".
The last is the amounts of seconds since 1th January 1970 00:00. The others are ingame dates.

```lua

local function eraseAnItem(theItem)

    world:erase(theItem, theItem.number)

end

```

#### `world:erase(scrItem item, number amount)`

Erase an amount of the input item.

"number", found in the Item.class documentation, can be particularly useful here.

```lua

local function increaseByOne(theItem)

    world:increase(theItem, 1)

end

```

#### `world:increase(scrItem item, number count)`

Used to increase the count of an item by a specified number.

```lua

local function swapItemWithBanana(theItem)

    --Swap the item with a banana while keeping the old quality
    world:swap(theItem, Item.banana, theItem.quality)

end

```

#### `world:swap(scrItem oldItem, number newItemID, number quality)`

Exchanges the old item with a new one of the new item ID of a specified quality, while keeping any other data values.

```lua

--Creates one singular banana of perfect quality and durability in front of the queen npc in Cadomyr, regardless of whether an item already exists on that field.
local theItem = world:createITemFromId(Item.banana, 1, position(122, 522, 0), true, 999, {["descriptionEn"] = "One outstanding banana fit for a queen."})

```

#### `scrItem world:createItemFromId(number itemID, number count, posStruct position, boolean occupied, number quality, dataTable data)`

Creates an item from the given ID, where the occupied boolean determines whether or not to create it if the field already has something on it. True and it ignores whether it is occupied, false and it won't create the item if it is occupied.

```lua

local function moveItem(theItem)

    local moveToPosition = position(122, 522, 0)
    world:erase(theItem)
    world:createITemFromItem(theItem, moveToPosition, true)

    --Moves theItem to in front of the queen npc in Cadomyr by copying the old one and deleting it, then putting a new one in its place at the new position
end
```

#### `world:createItemFromItem(scrItem item, posStruct position, boolean occupied)`

Unlike the above function that uses an item ID to create a new item, this one copies an existing item struct. It also doesn't return the new item, unlike what the previous function does, so you will have to fetch it manually via other means such as the world:getItemOnField function detailed below if you want to make further changes to it.

```lua

local theThief = world:createMonster(5, position(122, 522, 0), 100)

theThief:talk(Character.say, "Haha, I will steal your queen!")

--Spawns a human thief on the tile in front of the queen of Cadomyr, with 100 movepoints, who then speaks his given phrase.

```

#### `Character world:createMonster(number monsterID, posStruct position, number movepoints) `

Summons a monster with the given monster-ID at the given location, starting out with the given movepoints. You can find a list of monster-IDs in the database.

Returns the character structure of the monster you spawned.


```lua

local theQueen = world:createDynamicNPC("Rosaline Edwards", 0, position(122, 521, 0), 1, "npc.rosaline_edwards")

theQueen:talk(Character.say, "I am the queen. Obey me, peasants!")

```

#### `Character world:createDynamicNPC(text name, number race, posStruct position, number gender, text scriptName) `

Summons an npc with the given paramaters, using the script provided, returning the npc structure.

```lua

```
#### `??? world:deleteNPC(Character theNPC, ???)`

Delete a specified NPC?


```lua

local function aimCheck(user, target)

    local list = world:LoS(user.pos, target.pos)

    if list ~= nil then --the list exists
        for _, listEntry in pairs(list) do
        local theObject = listEntry.OBJECT
            if listEntry.TYPE == "ITEM" or listEntry.TYPE == "CHARACTER" then
                return false, listEntry.TYPE, theObject --There's a character or item blocking the way
            end
        end
    else
        return true --Nothing is blocking the way!
    end
end


local function damagePermissionCheck(user, target)

    local canTakeAim, blockedByType, blockedByObject = aimCheck(user, target)

    if not canTakeAim then
        if blockedByType == "ITEM" then
            user:inform("There are items obstructing your vision from taking aim.")
        else
            user:inform(blockedByObject.name.." is blocking your way, what a numbskull!")
        end
        return false
    end

    return true
end

```

#### `list world:LoS(posStruct startPosition, posStruct endPosition) `

If there are objects in the way between the start position and end position, it will return a list of these. These can be characters or items.

You can differentiate which is which by using .TYPE to find if it is a "CHARACTER" or "ITEM".

The item/character itself can be taken by using .OBJECT.



```lua

--Oh no, the queen has started making sheep sounds!

world:makeSound(2, position(122, 521, 0))

```

#### `world:makeSound(number soundID, posStruct position) `

Makes a sound of the corresponding ID at the given position. A list of sound effects can be viewed in the resources section on this site.

```lua

--Oh no, the queen is on fire!

world:gfx(36, position(122, 521, 0))
```

#### `world:gfx(number gfxID, posStruct position) `

Makes a graphical effect of the corresponding ID at the given position. A list of graphical effects can be viewed in the resources section on this site.

```lua

--gods save the queen, the floor underneath her chair has suddenly become lava!

world:changeTile(5, position(122, 521, 0))

```

#### `world:changeTile(number tileID, posStruct position) `

Changes the tile on the given position to the given tileID. A list of tiles can be viewed in the resources section on this site.

```lua

local function getDatabaseStatsFromItem(theItem)

    local databaseItemStats = world:getItemStats(theItem)

    return databaseItemStats

end

```

#### `comItem world:getItemStats(scrItem item) `

Allows you to fetch the ItemStruct variables from a target item. See the class ItemStruct in the list to the left to see which variables are available, as opposed to the Item class which details the variables available from a script item.

```lua

local function getDatabaseStatsFromItemID()

    local databaseItemStatsForBananas = world:getItemStats(Item.banana)

    return databaseItemStatsForBananas

end


```

#### `comItem world:getItemStatsFromId`

Same as the above function, except you can use it in cases when you know the item id of an item but do not have the actual script item of one.


```lua

local doesAnyItemExist = world:isItemOnField(position(122, 520, 0))

```

#### `boolean world:isItemOnField(posStruct position)`

Checks if there is an item on the field.

```lua

local function isTheQueensThroneEmpty(user)

    local doesAnyItemExist = world:isItemOnField(position(122, 520, 0))

    if not doesAnyItemExist then
        return nil
    end

    local theQueensThrone = world:getItemOnField(position(122, 520, 0))

    if not theQueensThrone.id ~= 2915 then --check if the topmost item is not a throne after all
        user:inform("What's this? Did someone put something on top of the queen's throne? Some pins as a prank, maybe?")
        return false
    end
    return true
end


```

#### `scrItem world:getItemOnField(posStruct position)`

Returns the topmost scriptItem that is on the field of the given position.


```lua

local function checkIfTheQueenIsThere()

    local sheIsThere = world:isCharacterOnField(position(122, 521, 0))

    if sheIsThere then
        return true
    end

    return false
end

```

#### `boolean world:isCharacterOnField(posStruct position) `

Checks if there is a character on the field.

```lua

local function fetchTheQueen()

    if checkIfTheQueenIsThere() then
        return world:getCharacterOnField(position(122, 521, 0))
    end

end

```

#### `Character world:getCharacterOnField(posStruct position)`

Returns the Character structure of the character standing on the field.

```lua

local function arePlayersNearTheQueen()

    local playersNearby = world:getPlayersInRangeOf(position(122, 521, 0), 5)

    if playersNearby then
        return true
    end

    return false
end

```

#### `list world:getPlayersInRangeOf(posStruct position, number range)`

Returns a list of any player character-structs within given range of tiles of the given position.

```lua

local listOfPlayersOnline = world:getPlayersOnline()

```

#### `list world:getPlayersOnline()`

Returns a list of all players who are currently online.


```lua

local charactersNearby = world:getCharactersInRangeOf(position(122, 521, 0), 3)

```

#### `list world:getCharactersInRangeOf(posStruct position, number range)`

The same as the above but with any characters(monsters, npc, players).

```lua
local npcsNearby = world:getNPCSInRangeOf(position(122, 521, 0), 3)
```

#### `list world:getNPCSInRangeOf(posStruct position, number range)`

The same as the above but with NPCs only.

```lua
```

#### `??? world:getNPCS(???)`

????

```lua
local monstersNearby = world:getMonstersInRangeOf(position(122, 521, 0), 3)
```

#### `list world:getMonstersInRangeOf(posStruct position, number range)`

The same as the above but with monsters only.

```lua

local function setOrUnsetPersistence(user, thePosition)

    if not world:isPersistentAt(thePosition) then
        world:makePersistentAt(thePosition)
        user:inform("The position was made persistent.")
    elseif world:removePersistenceAt(thePosition) then
        user:inform("The position is no longer persistent.")
    else
        user:inform("Error: Position was persistent but persistence could not be removed.")
    end

end

```

```lua

```
#### `world:getMonsterAttack(???)`

????


```lua

```

#### `world:setWeather(???)`

????

```lua

```

#### `world:createSavedArea(???)`

????

```lua

```

#### `world:sendMonitoringMessage(???)`

????

#### `boolean world:isPersistentAt(posStruct position)`

Checks if the field is persistent(more on that below).

#### `world:makePersistentAt(posStruct position)`

Makes the map persistent over server shutdowns and map imports at the given position. If no field exists at the given position, it is created empty.

#### `boolean world:removePersistenceAt(posStruct position)`

Removes persistence from a field at the given position. If no regular map exists there, the field is removed. In this case the server will clean up all characters on this field. Monsters and NPCs are removed, while players will be warped to a nearby field on the same level if possible, or to the starting position otherwise. The script is responsible for cleaning up the field before removal, since those defaults are generally not desirable for players.

```lua

local bananaNameInGerman = world:getItemName(Item.banana, Player.german)

```

#### `text world:getItemName(number itemID, number playerLanguage)`

Returns the item name that belongs to the item of the given item id, in the specified language.

Languages can be:
Player.german
Player.english

```lua
local function makeItemStatic(theItem)

    theItem.wear = 255
    world:changeItem(theItem)

end
```

#### `world:changeItem(scrItem item)`

If you want to change the writable values of a scrItem, such as wear, this is then used to reflect that change on the actual item.

```lua

local isWeapon, theWeaponStruct = world:getWeaponStruct(Item.halberd)

```

#### `boolean, wpnStruct world:getWeaponStruct(number itemID)`

Checks for whether or not an item by the given item ID is a weapon, and if so returns the weapon structure. See the weaponStruct class for more.

```lua
local isArmor, theArmorStruct = world:getArmorStruct(Item.plateArmour)
```

#### `boolean, armStruct world:getArmorStruct(number itemID)`

Checks for whether or not an item by the given item ID is a piece of armor, and if so retursn the armor structure. See the armorStruct class for more.

```lua

local doHumansHaveNaturalArmor, theNaturalArmorStructOfHumans = world:getNaturalArmor(0)

```

#### `boolean, natarmStruct world:getNaturalArmor(numer raceID)`

Returns whether the race has a natural armour and the natural armor structure of the given race if it does have one.

```lua
world:broadcast("Hallo!", "Hello!")
```

#### `world:broadcast(text germanText, text englishText`

Sends a broadcast to all players in the game, in the language of their account.



