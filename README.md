[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod-redirect-0.herokuapp.com/)

# Combat de personnages dans un jeu (chapitre 11)

<!-- Avant de commencer. Consulter les instructions à suivre dans [instructions.md](instructions.md) -->

Nous allons programmer une classe de personnage très simple qui permet d'effectuer des combats tour-à-tour dans un jeu.

## Armes des personnages
### `game.Weapon`

On veut une classe qui représente une arme. Une arme possède un nom, un niveau d'attaque et un niveau minimal pour l'utiliser.

Le nom ne peut pas être changé.

On veut une méthode de classe `make_unarmed` qui construit un `Weapon` nommé `"Unarmed"` avec une puissance de 20.

## Personnages du jeu
### `game.Character`

Dans notre jeu, un personnage est composé des propriétés suivantes :

`Character.name` : Le nom du personnage <br>
`Character.max_hp` : HP maximum <br>
`Character.attack` : Le niveau d'attaque du personnage <br>
`Character.defense` : Le niveau de défense du personnage <br>
`Character.level` : Le niveau d'expérience du personnage <br>
`Character.weapon` : L'arme utilisée par le personnage <br>
`Character.hp` : Les HP restants <br>

On a une méthode `compute_damage` qui calcule les dégâts infligés à un autre personnage (en paramètre). La formule est la suivante : 

<img src="doc/assets/dmg_eq.png" width="600">

Où *a* est l'attaquant et *d* est le défendeur. <br>
*crit* est 2 environ 1/16 (6.25%) du temps, 1 sinon <br>
*random* est un nombre aléatoire entre 85% et 100%

## Déroulement d'un combat

### `game.deal_damage()`

La fonction prend en paramètre le personnage attaquant et le personnage défendeur (dans cet ordre), calcule et applique le dommage, puis affiche ce qui s'est passé.

Exemple:
```python
c1 = Character("Äpik", 200, 150, 70, 70)
c2 = Character("Gämmor", 250, 100, 120, 60)

c1.weapon = Weapon("BFG", 100, 69)
c2.weapon = Weapon("Deku Stick", 120, 1)

deal_damage(c1, c2)
```

Sortie :
```
Gämmor used Deku Stick
  Äpik took 86 dmg
```

### `game.run_battle()`

La fonction prend en paramètre le personnage attaquant et le personnage défendeur (dans cet ordre) et exécute les attaques entre les personnages, tour-à-tour, jusqu'à ce qu'un des deux meurt (HP à zéro). La fonctio retourne le nombre total de tours effectués.

Exemple :
```python
c1 = Character("Äpik", 200, 150, 70, 70)
c2 = Character("Gämmor", 250, 100, 120, 60)

c1.weapon = Weapon("BFG", 100, 69)
c2.weapon = Weapon("Deku Stick", 120, 1)

turns = run_battle(c1, c2)
print(f"The battle ended in {turns} turns.")
```

Sortie :
```
Äpik starts a battle with Gämmor!
Äpik used BFG
  Gämmor took 70 dmg
Gämmor used Deku Stick
  Äpik took 82 dmg
Äpik used BFG
  Gämmor took 69 dmg
Gämmor used Deku Stick
  Äpik took 91 dmg
Äpik used BFG
  Gämmor took 67 dmg
Gämmor used Deku Stick
  Äpik took 83 dmg
Äpik is sleeping with the fishes.
The battle ended in 6 turns.
```