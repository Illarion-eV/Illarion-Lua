# Entry Points

As described in the [introduction](#introduction), entry points are the interface between server and scripts. The server
calls entry points on a variety of events to perform the implemented game mechanics. This allows the server to remain
unchanged and running, while scripts are updated at run-time.

Entry points are expected to be functions with pre-defined names, which the server will call. For the server to be able
to find the script these functions are in, the script is named in the db entry of the appropriate game entity. The only
exception are _server scripts_, which just have one exact name.

The server expects scripts to return a table, which contains all implemented entry points. In the following definitions
only the function signature is given for clarity.

Those scripts which are entered into the database, need to be named in the following format:

* Paths are relative to the repository base directory.
* Directory/file names are seperated by a full stop (`.`).
* The `.lua` extension is omitted.

E.g. a script `item/apple.lua` would be entered as `item.apple`.

Some scripts provide a special global service for the server. These scripts are not attached to a specific game object
(e.g. item, monster or field), but define general or in some cases default behaviour. All of these scripts are located
in the `server` directory. Server scripts should be edited with great caution, since breaking one of those scripts would
break the related behaviour for the server.

<aside class="info">
Database scripts are defined in a specific database table. Each server script is in a file with a pre-defined name.
</aside>