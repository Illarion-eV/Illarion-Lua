# Debugging

After setting up your editor as described in the [tutorial](#tutorial), it will tell you about Lua syntax errors and
other problems, like the use of global variables. However, some issues will only surface at run-time. If a script throws
an error while it is running, that error will appear in the server log.

With the local server you can view this log in the console you started the server in.

The Illarion [development server](https://illarion.org/~devserver/script_error_log.php) and the Illarion
[game server](https://illarion.org/~illarionserver/script_error_log.php) provide a summary of script errors. In these
logs error messages will start with the number of occurences of a specific error, followed by a time stamp.

## Functions

Crude mechanisms like sending debug or error messages to players and prompting them to contact a developer are not very
helpful, since you rely on the player to give a hopefully accurate report, if the report occurs at all. Instead there
are two functions you can use to send information to the server log.

### `debug(string message)`


```lua
debug("some debug info")
```
```
game-server_1  | Script (notice): Debug Message: some debug info
game-server_1  | #1 called by: /usr/share/illarion/scripts/test.lua:11

```

Sends a debug `message` to the server log, including a call stack which will show where the message came from. This is
disabled on the Illarion game server.

Notice how the server log will show your files in the server's script directory `/usr/share/illarion/scripts/` instead
of your local script directory. After the file name, seperated by a `:` you can see the line number.

### `error(string message)`

```lua
error("some error message")
```
```
game-server_1  | Script (err): /usr/share/illarion/scripts/test.lua:16: some error message
game-server_1  | #1 called by: [C]:-1(global error)
game-server_1  | #2 called by: /usr/share/illarion/scripts/test.lua:16
```

Sends an error message to the server log and **aborts** the current script. Use this to avoid running into undefined states
or to prevent potential loss of data. Just as with `debug` you will get a call stack, which will show the error's
origin.
