## Monsters

### `abortRoute(Character monster)`
Is called if `monster` has reached the destination of its route or if items block the way and the destination cannot
be reached. See section Waypoints in [Character](#character) for details on routes.

### `boolean actionDisturbed(Character user, Character disturber)`
Is called when `user` is attacked while an action is running. This action had to be started by `user:startAction(...)`
in `useMonster`. If this entry point does not exist or returns `false` the action is not aborted. If it returns `true`
the action is aborted. See section Actions in [Character](#character) for more details on starting actions.

### `boolean enemyNear(Character monster, Character enemy)`
Invoked when `monster` is on a field next to `enemy`. If `setTarget` returns `0` ("don't attack anyone"), then
`enemyNear` has to return `false`.

### `boolean enemyOnSight(Character monster, Character enemy)`
Invoked whenever a monster sees an enemy. Must return true or false.

It is not invoked when the monster stands on a field next to the enemy.

### `lookAtMonster(Character user, Character monster, number mode)`

Invoked when `user` looks at `monster` with `mode` being one of:

* `Player.look`: casual inspection
* `Player.stare`: thorough inspection

<aside class="info">
The current client does not support Player.look, so mode will always be Player.stare
</aside>

### `onAttack(Character monster, Character enemy)`
Invoked every time `monster` would hit `enemy`.

### `onAttacked(Character monster, Character attacker)`
Invoked when `monster` is hit by `attacker`.

### `onCasted(Character monster, Character caster)`
Invoked when a spell is cast on `monster` by `caster`.

<aside class="info">
The current client does not implement magic, so this entry point is never called.
</aside>

### `onDeath(Character monster)`
Invoked as `monster` dies.

### `onSpawn(Character monster)`
Invoked after `monster` has spawned.

### `receiveText(Character monster, number textType, string text, Character speaker)`
Invoked when `monster` receives `text` spoken by `speaker`. `textType` is `Character.say`, `Character.whisper` or
`Character.yell`.

### `number setTarget(Character monster, table candidateList)`
If `setTarget` exists, it is called whenever `monster` needs to decide what it should attack.
The `candidateList` is a table of [players](#character) who are possible targets.
To set a target, its index in that table has to be returned.
The first enemy in the table has the index `1`.
If the entry point returns `0`, `monster` will ignore all enemies.
If `setTarget` does not exist, the player with lowest health is chosen by default.

### `useMonster(Character monster, Character user, number actionState)`
A `user` uses a `monster`. `actionState` is one of

* `Action.none`: no action is running.
* `Action.success`: an action was running and has been completed.
* `Action.abort`: an action was running and has been interrupted by the user being attacked or the user doing something
else like using an item, moving, etc.

See section Actions in [Character](#character) for more details on starting actions.