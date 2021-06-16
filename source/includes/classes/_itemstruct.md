## ItemStruct

```lua
local itemStats = world:getItemStats(item)
local item.wear = itemStats.AgeingSpeed
world:changeItem(item)
```
>Reset item wear to its default

```lua
local itemStats = world:getItemStatsFromId(Item.apple)
local vendorSellPrice = itemStats.Worth
local nameEnglish = itemStats.English
local nameGerman = itemStats.German
```
>We don't need an actual item to get this data, the id (Item.apple) is enough.

Represents item definitions obtained from the database. Does not represent an item on the map or in a player's inventory,
but general information about an item with a specific id. 

### Variables

All of these variables are read-only.

Name               | Type     | Description
------------------ | -------- | -----------
AgeingSpeed        | number   | item does not decay for 3 * AgeingSpeed minutes, by default 
Brightness         | number   | from 0 to 9, used for light sources
BuyStack           | number   | default stack size on vendors
English            | string   | English item name
EnglishDescription | string   | English item description
German             | string   | German item name
GermanDescription  | string   | German item description
id                 | number   | item id
Level              | number   | item level from 0 to 100
MaxStack           | number   | maximum stack size
ObjectAfterRot     | number   | item id the item changes into after decaying
Rareness           | number   | ItemLookAt.commonItem, ItemLookAt.uncommonItem, ItemLookAt.rareItem or ItemLookAt.epicItem
rotsInInventory    | boolean  | if set, item decays in a player's inventory, useful for e.g. lit torches
Weight             | number   | item weight, item can only be moved if its weight is below 30000
Worth              | number   | sold by vendors for this amount of copper coins