### Character - Books
#### `sendBook(number id)`
```lua
character:sendBook(0)
```
Tells the client to display book `id` for the current character.
### Character - Item/Inventory handling
Relevant class sections for the following section :
[Item](#item), [ItemStruct](#itemstruct).
A full list of all item IDs can be found [here](https://illarion.org/~martin/itemlist.pdf).


* Inventory slots
The current implementation covers following inventory/ slot IDs.


| enum  | value |
|---|---|
| Character.backpack  | 0 |
| Character.head  | 1 |
| Character.neck  | 2 |
| Character.breast  | 3 |
| Character.hands  | 4 |
| Character.left_tool  | 5 |
| Character.right_tool  | 6 |
| Character.finger_left_hand  | 7 |
| Character.finger_right_hand  | 8 |
| Character.legs  | 9 |
| Character.feet  | 10 |
| Character.coat  | 11 |
| Character.belt_pos_1 | 12 |
| Character.belt_pos_2 | 13 |
| Character.belt_pos_3 | 14 |
| Character.belt_pos_4 | 15 |
| Character.belt_pos_5 | 16 |
| Character.belt_pos_6 | 17 |

#### `increaseAtPos(number bodyPosition, number count)`
```lua
character:increaseAtPos(Character.belt_pos_1,1)
```
Increases the amount of items at `bodyPosition`by `count`.

#### `swapAtPos(number bodyPosition, number itemID, number quality)`
```lua
-- 2763 == pickaxe
character:swapAtPos(Character.belt_pos_1, 2763, 999)
```
Changes the item at the given `bodyPosition` to the given `itemID` and `quality`.
A full list of all item IDs can be found [here](https://illarion.org/~martin/itemlist.pdf).

#### `table getItemList(number itemID)`
```lua
character:getItemList(2763)
```
Returns a list with all items of this `itemID`.

### Character - Depot/Containers

#### `conStruct getBackPack()`
```lua
character:getBackPack()
```
Returns a container-item, which can contain other items.

#### `conStruct getDepot(number depotID)`
```lua
character:getDepot(0)
```
Returns a container-item (the depot of that Character).

#### `table takeItemNr(number bodyPosition,number amount).`
```lua
character:takeItemNr(Character.belt_pos_2,2)
```
Takes the `amount` of items from the `bodyPosition` and returns the taken items.

### Character - Items

#### `number createItem(number itemID, number count, int number quality, dataTable data)`
```lua
character:createItem(2764, 1, 999, {})
```
Item is created in the belt or backpack of character. If that is not possible, the items will
not be created. The function returns an integer that gives the number of items that cannot
be created.

#### `createAtPos(number bodyPosition, number itemID, number count)`
```lua
character:createAtPos(Character.hands, 2763, 1)
```
Creates an item at a special body position.

#### `changeQualityAt(number bodyPosition, number amount)`
```lua
character:changeQualityAt(hands, 333)
```
Changes the quality by the  `amount` at the `body position`.

#### `number eraseItem(number itemID, number count)`
#### `number eraseItem(number itemID, number count, table data)`
```lua
character:eraseItem(2763, 1, {})
character:eraseItem(2763, 1, {glyphEffect:0})
```
The given `count` of items with the `itemID` are erased from the inventory. You have
no influence on which items are deleted, you can just determine ID and number. The return
value contains the amount of items that could not be deleted. In case the optional `data`
parameter is set, only items that include these data values are deleted. If the data table is
empty however, only items without data are erased.

#### `number countItem(number itemID)`
```lua
character:count(2763)
```
Returns the amount of items with type `itemID` in the character's inventory.
#### `number countItemAt(string slots, number itemID)`
#### `number countItemAt(string slots, number itemID, table data)`
```lua
character:countItemAt("all", 2763)
character:countItemAt("all", 2763, {"madeBy": "Vilarion"})
```
Counts only at the specified `slots`
Valid `slots` values are  "all", "belt", "body", "backpack". The variant with `data` does only count
items that include these data values. If the data table is empty however, only items without
data are counted.
