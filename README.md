# PacMan

Durant ce TP vous allez apprendre à :
  - manipuler les lists
 - les bases de la programmation orientée objet
 - Créer une IA

Vous allez être amenés à utiliser la librairie python **pygame** pour ceci il vous faut travailler sur un shell après avoir exécuter la commande suivante :

```sh
nix-shell -p python311Packages.pygame
```

Vos outils:

Vous disposez d'une classe Pacman:
les attributs que vous utiliserez sont:
-self.size -> le nombre de pixel par case
-self.speed -> la vitesse du Pacman
-self.life -> les points de vie
-self.dt -> le delta de temps (expliqué plus bas)
-self.pos.x -> la position sur l'axe des abscisses
-self.pos.y -> la position sur l'axe des ordonnées
-self.score -> le score
-self.power_up -> booléen indiquant si le power up est actif (booléen signifie que la variable peut être soit vrai ou fausse)
-self.timer -> la durée de récupération du power up

## Partie 1: src/pacman.py

### Le mouvement

Pour commencer, voyons le mouvement. Vous allez devoir implementer le déplacement de Pacman dans 4 directions.
Ici nous vous proposons de diviser les différents mouvements en sous fonction pour la lisibilité du code (vous pouvez rajouter autant de sous fonction que vous désirez pour alléger le code)

pour adapter le mouvement a la fréquence d'image et que la puissance du PC n'impact pas la rapidité du jeu nous utilisons une variable **dt** qui est un delta du temps permettant de synchroniser la fréquence d'image avec le temps qui s'écoule.

pour utiliser ce delta, il suffit de multiplier la variable ajoutée à votre position par **dt** comme ceci:

```py
self.pos.x += self.speed * self.dt
```

Tips: Pour gérer le mouvement, nous vous conseillons de calculer les coordonnées d'arrivé puis de mettre à jour la position du Pacman. De cette manière vous pourrez par la suite vérifier si votre position est valide ou non (pour les collisions avec les murs).

La formule pour convertir les déplacements : nouveau_x = vieux_x / taille_case


Une fois que votre Pacman peut se déplacer dans toutes les directions, vous allez pouvoir vous pencher sur les collisions.


### PacMan.kill()
Cette fonction est appelée quand le Pac-Man est tu et doit réduire la vie de 1, réinitialiser la position à celle de départ.

### PacMan.eat()
Cette fonction permet de manger les petits points blancs afin de gagner des points, il faut donc vérifier si l'on peut manger le point et ensuite ajouter les points.
s'il s d'un point spécial il faut mettre le Pac-Man en mode Power *True*

### PacMan.Power()
Cette fonction doit permettre à Pac-Man de garder son powerup durant environ dix secondes. Pour ce faire vous pouvez utiliser la librairie time de python et de la fonction timer de cette librairie.

## Partie 2: src/maze.py src/utils.py

### src/maze.py
Ici rien de très compliqué la génération du labyrinthe est donné, il manque la méthode **Maze.check_end** qui renvoie *False* s'il n'y a plus de point à récupérer dans le labyrinthe *True* sinon.

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
