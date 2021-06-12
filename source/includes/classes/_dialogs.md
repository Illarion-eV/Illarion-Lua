## Dialogs

Dialogs are a more sophisticated approach to aquire user input than e.g. `user.lastSpokenText`. Each dialog serves a
specific purpose like displaying bulk text, interfacing with a merchant or with the crafting system. Dialogs should be
the preferred method for handling user input. If necessary new types should be implemented rather than abusing old
variants or falling back to `lastSpokenText`. Please note, that as with many functions dialogs work with all types of
characters (players, monsters, npcs) but only make sense with players. Using the other two types will work but do
nothing at all. Using a dialog always consists of three descrete steps:

1. Create a callback function to be triggered automatically when the user closes the dialog. This function has to have a
single parameter to which the dialog will be passed with obtained results.
2. Invoke the constructor of a specific dialog to create a dialog instance, passing required parameters and callback.
3. Have a player object request the dialog in the user's client. Script execution does not stop after this request. The
callback with results is called whenever the user closes the dialog.

Usually, creating an object would be described before talking about results. However, here we chose a different order to
follow the three steps mentioned above, which reflect the order in which you would write a dialog, and to review the
most interesting details first, namely what each dialog actually contributes to a particular script.