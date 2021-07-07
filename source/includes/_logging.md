# Logging

Sometimes you want to log information e.g. for game masters. You can do this with the `log` function.

With the local server you can view this log in the console you started the server in.

The Illarion [development server](https://illarion.org/~devserver/script_log.php) and the Illarion
[game server](https://illarion.org/~illarionserver/script_log.php) provide a summary of this log. In these
logs messages will start with the number of occurences of a specific entry, followed by a time stamp. Be aware of the
fact that these logs are publicly available.

## Functions

### `log(string message)`


```lua
log("some information")
```
```
game-server_1  | Script (info): some information
```

Sends a log `message` to the server log.