## Container

```lua
local M = {}

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

local function changeQualityAt(user, theDepot)

    local success, theItem = theDepot:viewItemNr(1)

    if success then
        local oldQuality = theItem.quality
        local qualityChanged = theDepot:changeQualityAt(1, 333)
        success, theItem = theDepot:viewItemNr(1)
        if qualityChanged and success then
            local newQuality = theItem.quality
            user:inform("An item with an ID of "..theItem.id.." had it's quality changed from "..oldQuality.. " to "..newQuality..".")
        end
    end

end

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

local function insertItem(user, theDepot)

    local success, theItem = theDepot:viewItemNr(1)

    if success then
        theDepot:insertItem(theItem, true)
    end

end

local function countItem(user, theDepot)

    local numberOfRegularScissors = theDepot:countItem(6)
    local numberOfSpecialScissors = theDepot:countItem(6, {nameEn = "Special Scissor"})

    user:inform("There are "..numberOfRegularScissors.." regular scissors and "..numberOfSpecialScissors.. " special scissors in the container.")

end

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

local function increaseAtPos(user, theDepot)

    theDepot:increaseAtPos(1, 40)

end

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

local function getWeight(user, theDepot)

    local weight = theDepot:weight()

    user:inform("The container weighs a total of "..weight.. " weight units.")

end

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



Containers are items that can contain other items. Examples of these are a character's backpack and depot. 

### Functions

#### `boolean, scrItem, conStruct Container:viewItemNr(int (itempos))`
Returns a boolean for success, the item found at the given position if any, as well as the container if the item found is a container item.
The "itempos" can be anything from 0-99, signifying the corresponding slot in the container from left to right, top to bottom.
Most containers have 100 slots in total, however some cases such as the "basket" item have less.

#### `boolean, scrItem, conStruct Container:takeItemNr(int (itempos), int (count))`
Returns the same values as the above viewItemNr function, but it also deletes an amount of the item. How many it deletes is determined by the count integer.

#### `Container:changeQualityAt(int (itempos), int(amount))`
This function is supposed to change the quality of the item at the given position inside the container to whatever the amount integer is set to. It returns as true if it worked.
The quality value of an item is a three digit  integer, where the first digit corresponds to quality (0-9) and the latter digits correspond to durability (00-99).
For some reason, this function does not work currently.
Related issue: https://github.com/Illarion-eV/Illarion-Server/issues/81

#### boolean `boolean Container:insertContainer(scrItem (item), conStruct (container), int (itempos))`

If itempos has been provided, tries to insert a container at that position. If not, or if that position is not free, inserst the container at the first free position. Returns true if successful.

#### `Container:insertItem(scrItem (item), boolean (merge))`
Inserts an item into the container. 
If merge is false, it inserts the item in the first available slot of that container.
If merge is true, it will insert into an existing stack of said item if it exists.

#### `int void Container:countItem(int (itemid), dataTable (data))`
Counts the number of items in a container of a given ID, including items that may be inside containers inside said container.
The data parameter is optional. If the data parameter is set, only items that include these data values are counted. If the data table is empty, only items without data are counted.

#### `int void Container:eraseItem(int (itemid), int (count), dataTable (data))`
Erases an amount of the specified item that is the same as the count integer from the container. If a datatable is specified, it will only erase items with data that matches that. If no datatable is specified, it will only erase items with no special data. The returned integer is how many items could not be deleted.

#### `Container:increaseAtPos(int (itempos), int (value))`
Increase the number of items at a given position.
It should return the number of items increase, but currently it does not.
Related issue: https://github.com/Illarion-eV/Illarion-Server/issues/82

#### `boolean void Container:swapAtPos(int (itempos), int(newId), int(newQuality))`
Changes the ID and quality of an item.
Returns true on success.
Here it's also important to make sure the item stack number is correct. You don't want to suddenly have a stack of normally unstackable items.

#### `int void Container:weight()`
Returns the total weight of that container.
