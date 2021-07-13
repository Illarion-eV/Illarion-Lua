### "Character - Actions"

### `performAnimation(number animation)`
```lua
//11 = Casting animation.
character:performAnimation(11)
```
Performs an `animation` for the current character.

### `boolean actionRunning()`
```lua
character:actionRunning()
```
Returns `true`if a character is currently performing an action,
otherwise `false`.

### `startAction(number wait, number animation, number redoAnimation, number sound, number redoSound)
```lua
 User:startAction(sanddigging.SavedWorkTime[User.id], GFX, sanddigging.SavedWorkTime[User.id], SFX, sanddigging.SavedWorkTime[User.id])
 ```
### `abortAction()`
Aborts the current action.
### `successAction()`
Terminates the current action.
### `disturbAction()`
Disturbes the current character from an action.
### `changeSource(item sourceItem)`
### `changeSource(position sourcePosition)`
### `changeSource(character sourceChar)`
Changes the source variable of the entrypoint used for subsequent calls of the current action. This has to be called explicitly to propagate changes of a source object to the action.
### `changeTarget(item targetItem)`
### `changeTarget(position targetPosition)`
### `changeTarget(character targetChar)`

Changes the target variable of the entrypoint used for subsequent calls of the current action.
<!-- TODO: -->