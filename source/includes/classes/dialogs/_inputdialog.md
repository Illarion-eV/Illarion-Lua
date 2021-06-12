### InputDialog

This dialog requests text input from the user. If you want to further restrict the input, make that clear to the user
using the description and enforce it inside the callback. For different kinds of input (e.g. items) use or request
development of a different type of dialog.

```lua
local callback = function(dialog)
    if not dialog:getSuccess() then
        user:inform("You canceled! How dare you?")
    else
        user:inform("You wrote: " .. dialog:getInput())
    end
end

local dialog = InputDialog("Insert some text!", false, 255, callback)
user:requestInputDialog(dialog)
```

#### Results

##### `boolean getSuccess()`

The result is `true` if the dialog was confirmed and `false` if it was aborted.

##### `string getInput()`

Returns the user's input if the dialog was successful. The return value is undefined if the dialog was aborted.

#### Construction

##### `InputDialog(string title, string description, boolean multiline, number maxChars, function callback)`

Creates an InputDialog with `title` and `description`. It allows line breaks iff `multiline` is set to `true`.
The input can be up to `maxChars` characters long.

#### Request

##### `user:requestInputDialog(InputDialog dialog)`