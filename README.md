# PacMan

Durant ce TP vous allez apprendre à :
  - manipuler les lists
 - les bases de la programmation orientée objet
 - Créer une IA

Vous allez être amenés à utiliser la librairie python **pygame** pour ceci il vous faut travailler sur un shell après avoir exécuter la commande suivante :

```sh
nix-shell -p python311Packages.pygame
```

### Vos outils:

Vous disposez d'une classe Pacman:
les attributs que vous utiliserez sont:\
-self.size -> le nombre de pixel par case\
-self.speed -> la vitesse du Pacman\
-self.life -> les points de vie\
-self.dt -> le delta de temps (expliqué plus bas)\
-self.pos.x -> la position sur l'axe des abscisses\
-self.pos.y -> la position sur l'axe des ordonnées\
-self.score -> le score\
-self.power_up -> booléen indiquant si le power up est actif (booléen signifie que la variable peut être soit vrai ou fausse: *True*/*False*)\
-self.timer -> la durée de récupération du power up

La carte se présente sous la forme de deux matrices:
La première : self.maze.maze -> ce tableau est peuplé de 1 et de 0, les 1 sont des murs et les 0 sont des sols.
ne vous laissez pas intimider par le terme matrice, c'est très simple: pour accéder à une case il suffit d'utiliser la synthaxe suivante:\
prenons la case en i = 5 et en j = 7 dans le maze:
self.maze.maze[7][5]

La deuxième matrice : self.maze.point -> ce tableau contient les points à manger pour le Pacman (2 pour les popwer-ups, 1 pour les point, 0 sinon).

Point à savoir: votre Pacman possède des coordonnés(pos.x et pos.y) qui représente sa position à l'échelle des pixels.
Vous devrez donc convertir ces coordonnées pour pouvoir lier les coordonnés du Pacman avec les matrices du maze (c'est à cela que sert self.size)

(si vous n'êtes pas sûr d'avoir compris certaines notions, demandez nous, on ne mord pas)\

Tous ces attributs sont des variables que vous devrez modifier pour faire fonctionner le jeu

## Partie 1: src/pacman.py

### Le mouvement

Pour commencer, voyons le mouvement. Vous allez devoir implementer le déplacement de Pacman dans 4 directions.
Ici nous vous proposons de diviser les différents mouvements en sous fonction pour la lisibilité du code (vous pouvez rajouter autant de sous fonction que vous désirez pour alléger le code). Ici vous devrzez donc manipuler self.pos.x et self.pos.y.\
Pour adapter le mouvement a la fréquence d'image et que la puissance du PC n'impact pas la rapidité du jeu nous utilisons une variable **dt** qui est un delta du temps permettant de synchroniser la fréquence d'image avec le temps qui s'écoule.

pour utiliser ce delta, il suffit de multiplier la variable ajoutée à votre position par **dt** comme ceci:

```py
self.pos.x += self.speed * self.dt
```

Tips: Pour gérer le mouvement, nous vous conseillons de calculer les coordonnées d'arrivé puis de mettre à jour la position du Pacman. De cette manière vous pourrez par la suite vérifier si votre position est valide ou non (pour les collisions avec les murs).

Une fois que votre Pacman peut se déplacer dans toutes les directions, vous allez pouvoir vous pencher sur les collisions. Vous allez devoir utiliser self.maze.maze pour cela vous allez devoir convertir les coordonnées du pacman pour savoir où vous vous situez dans le labyrinthe.\
La formule pour convertir les déplacements: index = vieux_x / taille_case

Maintenant que vous avez prit vos marques, voicis quelques fonctions que vous devez recoder afin de compléter le code du jeu:

### PacMan.kill()
Cette fonction sera appelée quand le Pac-Man est touché.\
La Pacman perd 1 point de vie et il revient à la position de départ (donnée par self.start_pos()).

### PacMan.eat()
Cette fonction permet de manger les petits points blancs afin de gagner des points.\
il faut donc d'abord vérifier si il y a un point à la position du Pacman (dans self.maze.point , voir plus haut) et augmenter le score.
s'il s'agit d'un power up il faut mettre le Pac-Man en mode Power *True*.

### PacMan.Power()
Cette fonction doit permettre à Pac-Man de garder son powerup durant environ dix secondes. Pour ce faire vous pouvez utiliser la librairie time de python et de la fonction timer de cette librairie (demandez des précisions à Titouan si c'est flou (le grand avec des cheveux longs, il est grave sympa)). Rappel: self.timer permet de gérer la durée.

## Partie 2: src/maze.py src/utils.py

### src/maze.py
Ici rien de très compliqué la génération du labyrinthe est donnée, il manque la méthode **Maze.check_end** qui renvoie *False* s'il n'y a plus de point à récupérer dans le labyrinthe *True* sinon.

### src/utils.py
Ce fichier permet d'avoir 2-3 fonctions utiles au programme qui ne nécessite pas de fichier à part entière.

#### check_hitbox(player, gh)
Test si le pacman est en collision avec un des fantômes et appele check event pour résoudre la collision et tuer l'un des deux
de plus la fonction renvoie *False* si la partie est finie, *True* sinon

## Partie 3: ghost.py

### le mouvement
De meme qu'avec pacman implementer les diferent methode de deplacement.

### Ghost.action()
Implémentez une IA basique ou plus évoluent pour que les fantômes choisissent leurs prochains déplacements.
Pour essayer votre code vous pouvez ajouter un déplacement aléatoire et ensuite chercher un déplacement plus fluide et intelligent
