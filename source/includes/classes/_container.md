## Container

Containers are items that can contain other items. Examples of these are a character's backpack and depot. 

```lua
local M = {}
```

### Functions

#### `boolean, Item, Container viewItemNr(number itempos)`

```lua

local function viewItemNr(user, theDepot)

    local success, theItem, theContainer = theDepot:viewItemNr(1)

    local text

    if success then
        if theContainer then
            text = "The item is a container with an item-ID of "..theItem.id
        else
            text = "The item is not a container. Its item-ID is "..theItem.id
        end
        user:inform(text)
    end
end
```

Returns a boolean for success, the item found at the given position if any, as well as the container if the item found is a container item.
The "itempos" can be anything from 0-99, signifying the corresponding slot in the container from left to right, top to bottom.
Most containers have 100 slots in total, however some cases such as the "basket" item have less.

#### `boolean, Item, Container takeItemNr(number itempos, number count)`

```lua
local function takeItemNr(user, theDepot)

    local success, theItem, theContainer = theDepot:takeItemNr(1, 1)

    local text

    if success then
        if theContainer then
            text = "A container with an item-ID of "..theItem.id.." was removed from the container."
        else
            text = "An item with an ID of "..theItem.id.." was removed from the container."
        end
    end

    user:inform(text)
end
```

Returns the same values as the above viewItemNr function, but it also deletes an amount of the item. How many it deletes is determined by the count integer.

#### `changeQualityAt(number itempos, number amount)`

```lua
local function changeQualityAt(user, theDepot)

    local success, theItem = theDepot:viewItemNr(1)

    if success then
        local oldQuality = theItem.quality
        local wantedQuality = 999
        local changeNeeded = wantedQuality - oldQuality
        local qualityChanged = theDepot:changeQualityAt(1, changeNeeded)
        success, theItem = theDepot:viewItemNr(1)
        if qualityChanged and success then
            local newQuality = theItem.quality
            user:inform("An item with an ID of "..theItem.id.." had it's quality changed from "..oldQuality.. " to "..newQuality..".")
        end
    end

end
```

This function changes the quality of the item at the given position inside the container by whatever the amount integer is set to. It returns as true if it worked.
The quality value of an item is a three digit  integer, where the first digit corresponds to quality (0-9) and the latter digits correspond to durability (00-99).
If the amount integer + the quality the item already is equals to higher than the maximum quality of 999 then the quality will not be changed while the durability will be set to the maximum of 99.

#### `boolean insertContainer(Item item, Container container, number itempos)`

```lua
local function insertContainer(user, theDepot)
    local success, theItem, theContainer = theDepot:viewItemNr(1)

    if success then
        if theContainer and theItem then
            success, theItem, theContainer = theDepot:takeItemNr(1, 1)
            if success then
                local containerInserted = theDepot:insertContainer(theItem, theContainer, 2)
                if containerInserted then
                    user:inform("Container has been inserted into the slot.")
                end
            end
        end
    end
end
```

If itempos has been provided, tries to insert a container at that position. If not, or if that position is not free, inserst the container at the first free position. Returns true if successful.

#### `insertItem(Item item, boolean merge)`

```lua
local function insertItem(user, theDepot)

    local success, theItem = theDepot:viewItemNr(1)

    if success then
        theDepot:insertItem(theItem, true)
    end

end
```
Inserts an item into the container. 
If merge is false, it inserts the item in the first available slot of that container.
If merge is true, it will insert into an existing stack of said item if it exists.

#### `number countItem(number itemid, Table data)`

```lua
local function countItem(user, theDepot)

    local numberOfRegularScissors = theDepot:countItem(6)
    local numberOfSpecialScissors = theDepot:countItem(6, {nameEn = "Special Scissor"})

    user:inform("There are "..numberOfRegularScissors.." regular scissors and "..numberOfSpecialScissors.. " special scissors in the container.")

end
```

Counts the number of items in a container of the given itemid, including items that may be inside containers inside said container.
The data parameter is optional. If the data parameter is set, only items that include these data values are counted. If the data table is empty, only items without data are counted.

#### `number eraseItem(number itemid, number count, Table data)`

```lua
local function eraseItems(user, theDepot)

    local amountToDelete = 10

    local amountFailedToDelete = theDepot:eraseItem(6, amountToDelete)

    if amountFailedToDelete == 0 then
        user:inform("All "..amountToDelete.." scissors were erased from the container.")
    else
        local deletedScissors = amountToDelete-amountFailedToDelete
        if deletedScissors > 0 then
            user:inform("Only "..deletedScissors.." scissors were erased from the container.")
        else
            user:inform("No scissors were erased from the container.")
        end
    end

end
```

Erases an amount of the specified itemid that is the same as the count integer from the container. If a Table is specified, it will only erase items with data that matches that. If no Table is specified, it will only erase items with no special data. The returned integer is how many items could not be deleted.

#### `increaseAtPos(number itempos, number value)`

```lua
local function increaseAtPos(user, theDepot)

    local itemPosition = 37

    local success, theItem = theDepot:viewItemNr(itemPosition)
    
    local oldAmount
    local itemId

    if success then
        oldAmount = theItem.number
        itemName = theItem.id
    else
        return --no item was found
    end

    local amountToAdd = 40
    local newTotalAmount = theDepot:increaseAtPos(itemPosition, amountToAdd)

    user:inform("You've added "..newTotalAmount-oldAmount.." out of the set "..amountToAdd.." requested additions to the item in slot "..itemPosition.." with the id of "..itemId.." making for a total of "..newTotalAmount.." from the previous "..oldAmount)
end
```
Increase the number of items at the given itempos by value, returning the new amount if upon success.
If the total number exceeds the stack limit of the items, only enough to reach the stack limit will be added.
This function also works with negative numbers to subtract item amounts instead.

#### `boolean swapAtPos(number itempos, number newId, number newQuality)`

```lua
local function swapAtPos(user, theDepot)

    local success, theItem = theDepot:viewItemNr(0)

    if success then
        if theItem.number == 1 then
            local swapItem = theDepot:swapAtPos(0, 9, 999)
            if swapItem then
                user:inform("The item in slot 0 was replaced with a saw and the quality was set to 999")
            end
        end
    end
end
```

Changes the ID of the item at itempos to newId and quality of the item to newQuality.
Returns true on success.
Here it's also important to make sure the item stack number is correct. You don't want to suddenly have a stack of normally unstackable items.

#### `number weight()`

```lua
local function getWeight(user, theDepot)

    local weight = theDepot:weight()

    user:inform("The container weighs a total of "..weight.. " weight units.")

end

```

Returns the total weight of that container.

```lua
function M.mainFunction(user, sourceItem, ltstate)

    local theDepot = user:getDepot(101) --Runewick's depot

    if theDepot then

        --[[It's important to check if the container exists. 
        For instance, a depot that has never been accessed does not exist for that character.]]

        myFunction(user, theDepot)

    end
end

return M
```
