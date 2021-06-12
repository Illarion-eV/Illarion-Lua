### MessageDialog

Use this dialog to display bulk text in an on-screen window. The user can close the window at any time.

```lua
local callback = function(dialog)
    user:inform("Dialog closed")
end

local lyrics = [[
O Fortuna
Velut luna
Statu variabilis
...
]]

local dialog = MessageDialog("O Fortuna", lyrics, callback)
user:requestMessageDialog(dialog)
```

#### Results

This type of dialog by it's very nature has no results to be accessed. Still a callback makes sense, because you might
want to react to the dialog being closed.

#### Construction

##### `MessageDialog(string title, string message, function callback)`

Creates a MessageDialog with a specific `title` and `message`.

#### Request

##### `user:requestMessageDialog(MessageDialog dialog)`