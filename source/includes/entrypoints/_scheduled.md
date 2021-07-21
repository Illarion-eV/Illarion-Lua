## Scheduled

```sql
INSERT INTO scheduledscripts VALUES ('SCRIPT_NAME', MIN_TIME, MAX_TIME, 'myScheduledFunction');
```

```lua
local M = {}

function M.myScheduledFunction()
    -- What I want my scheduled function to do
end

return M
```
**Database Table:** `scheduledscripts`

Scripts can be scheduled to be executed at defined intervals by entering them into the database.

You need the following information:

**Script name**

The name of the script file.

**Minimum Cycle Time**

The minimum time between each function call in deciseconds.

**Maximum Cycle Time**

The maximum time between each function call in deciseconds.
Can be set to the same value as minimum time to have no randomness.

**Function Name**

The name of the function you want to run.

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
|scheduled.myScript| 100| 150| informUsers| 

The above database entry will make it so that the function `informUsers` found in
`myScheduledScript.lua` in the `scheduled` directory is run every 10 to 15 seconds. In this case it is broadcasting
the given text to all players.