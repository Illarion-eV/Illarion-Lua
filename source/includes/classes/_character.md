## Character

Players, NPCs and monsters are the three types of characters in Illarion.

![directions](images/directions.png)

### Variables

Name           | Type     | Writable  | Description
-------------- | -------- | --------- | -----------
id             | number   | no        | character id
name           | string   | no        | character name
pos            | position | no        | character position on world map
lastSpokenText | string   | no        | character's last spoken line of text
attackmode     | boolean  | no        | `true` if character currently attacks, `false` otherwise
activeLanguage | number   | yes       | 0: common, 1: human, 2: dwarf, 3: elf, 4: lizard, 5: orc, 6: halfling, 7: fairy, 8: gnome, 9: goblin, 10: ancient
movepoints     | number   | yes       | A character has a maximum of 21 movepoints. Every action like talking, fighting, using etc. needs at least 7 movepoints. The reduction of movepoints depends on the character's agility. A character gains one movepoint per decisecond.

### Text/Speech Functions

#### `talk(number mode, string message)`
```lua
character:talk(Character.say, "Hello World!")
```
Lets a character say/whisper/yell a `message`. `mode` can be `Character.say`, `Character.whisper` or `Character.yell`.
