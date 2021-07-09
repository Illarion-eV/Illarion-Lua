### Character - Quests
#### `setQuestProgress(number questID, number progress)`
```lua
character:setQuestProgress(100,1)
```
A quest `progress` can be set for a specific `quest`.

#### `number getQuestProgress(number questID)`
```lua
character:getQuestProgress(100)
```
Returns the progress for a specific `quest`. Optionally also returns the time when this
progress was last set as Unix timestamp.
