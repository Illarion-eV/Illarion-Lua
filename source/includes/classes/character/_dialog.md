### Character - Displaying Dialogs
Please refer to the dialog chapter for building dialogs and for retrieving the interaction results.
#### `requestInputDialog(inputDialog dialog)`
```lua
character:requestInputDialog(InputDialog("Spawn Mob Selection",
                                    "Enter the range for the spawn area\nCurrent range: "..tostring(gmGetSpawnRange(item)).." tiles",
                                    false, 255, thisInputDialog))
```
#### `requestMessageDialog(messageDialog dialog)`
```lua
character:requestMessageDialog(MessageDialog("Tutorial", dialogText, callbackNewbie))
```
#### `requestMerchantDialog(merchantDialog dialog)`
```lua
character:requestMerchantDialog(MerchantDialog(common.GetNLS(player, "Handel", "Trade"), callback))
```
#### `requestSelectionDialog(selectionDialog dialog)`
```lua
character:requestSelectionDialog(SelectionDialog(caption, description, callback))
```
#### `requestCraftingDialog(craftingDialog dialog)`
```lua
character:requestCraftingDialog(CraftingDialog(self:getName(user), self.sfx, self.sfxDuration, callback))
```
Displays the defined `dialog` to the current character.

#### `sendBook(number id)`
```lua
character:sendBook(0)
```
Tells the client to display book `id` for the current character.