## Scheduled
```lua
local M = {}
function M.myScheduledFunction()
    -- What I want my scheduled function to do
end
return M
```
**Database Table:**`scheduledscripts`

Scripts can be scheduled to be executed at defined intervals by entering them into the database.

The entries can be separated into the following:

**Script name**

The name of the script file.

**Minimum Cycle Time**

The minimum time between each time the script is run, in seconds.

**Max Cycle Time**

The maximum time between each time the script is run, in seconds.

Can be set to the same as minimum time to have no randomness.

**Function Name**

The name of the function in the script that you want to run.

**Database entry example:**

```lua
local M = {}
function M.informUsers()
    world:broadcast("German Text","English Text")
end
return M
```

|sc_scriptname|sc_mincycletime|sc_maxcycletime|sc_functionname|
|-------------|---------------|---------------|---------------|
|scheduled.myScript| 10| 15| informUsers| 

The above database entry will make it so that the function called "informUsers" found in the lua script "myScheduledScript.lua" in the folder named "scheduled" is ran every 10 to 15 seconds, in this case broadcasting to every player whatever the input text is.