# Common Bugs

* Missing `end`, missing `(` or `)`
* Script name and db entry do not match (be careful of invisible characters!).  
  Try to query the db like this: `SELECT FROM illarionserver.items WHERE itm_script='item.doors')`.  
  `.` is used to seperate directory/file names and the `.lua` extension is omitted.
* Mixing up seperators `.` (fields) and `:` (member functions).
* Missing `()` for functions without parameters.
* Incorrect number of parameters for functions.
* Mispelled function names (use syntax highlighting!).
* Forgot !fr in game to reload tables and scripts.
* `=` instead of `==` or vice versa.
* `!=` instead of `~=` (not equal).
* Missing conversion of a string to a number (`local ten = tonumber("10")`).
* Beware of endless loops, they freeze the server. Always ensure that the script terminates.
* Instructions after `return`.
* Missing `then` in `if`-blocks, missing `end` in inline-`if`.
