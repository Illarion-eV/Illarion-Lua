## Monsters

**function onDeath(monster)**

Invoked as a monster dies.

**function receiveText(monster, textType, text, originator)**

Invoked when a monster receives spoken text.

**function onAttacked(monster, attacker)**

Invoked when a monster is attacked.

**function onCasted(monster, caster)**

Invoked when a spell is cast on a monster.

**function useMonster(monster, user)**

Invoked when a monster is used by user.

**function onAttack(monster, enemy)**

Invoked every time a monster would hit the enemy.

**function enemyOnSight(monster, enemy)**

Invoked whenever a monster sees an enemy. 

Must return true or false.

It is not invoked when the monster stands on a field next to the enemy.

**function enemyNear(monster, enemy)**

Same as enemyOnSight but when the monster is on the field next to it.

If you plan to have setTarget(...) return 0 ("don't attack anyone"), then enemyNear(...) must return false.

**function lookAtMonster(SourceCharacter, monster, mode)**

Invoked if the player looks at the monster.

Modes:

0 = normal

1 = close examination

**function onSpawn(monster)**

Invoked after the monster has spawned.

**function setTarget(monster, candidateList)**

If setTarget exists, it is called whenever the monster needs to decide what it should attack.

The candidateList is a list of players who are possible targets. 

To set a target, its index in that list has to be returned. 

The first enemy in the list has the index 1. 

If the function returns 0, the monster will ignore any enemy. 

If setTarget does not exist, the player with lowest health is chosen by default.

