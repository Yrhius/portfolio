+++
title = '6. Projet: Coder le jeu de société Trains en Java'
+++

Lors de mon deuxième semestre de BUT Informatique à Montpellier, j'ai eu l'occasion de coder Trains en binome avec un collège.

## Présentation du jeu

Trains est un jeu de société complexe mêlant jeu de plateau et jeu de cartes. Chaque joueur incarne une compagnie ferroviaire qui cherche à étendre son terrain d'activité au Japon. Le but est donc de gagner des point de victoire en construisant des gares, en construisant des rails sur des villes et des points d'intérêts ou encore en achetant des cartes victoire telle que des immeubles ! 

À son tour, un joueur commence par piocher 5 cartes de son paquet de cartes. Il peut ensuite jouer autant de cartes qu'il le souhaite, acheter autant de cartes qu'il souhaite puis ajoute dans sa défausse, les cartes jouée, achetée et inutilisée de sa main. Son tour est alors terminé, le joueur suivant pioche alors 5 cartes de sa propre pioche et ainsi de suite.

La partie s'arrête lorsque trois piles de cartes de la réserve ont été vidées ou lorsqu'un joueur a posé tous ses pions rails.
Le joueur qui cumule le plus de point victoire remporte la partie.

## Implémentation de l'algorithmique 

Nous sommes parties sur un squelette de code fourni par l'équipe enseignante. Ce squelette comprenait une interface graphique temporaire nous permettait de vérifier le bon fonctionnement de notre code. 

Il fallait dans un premier temps, coder chacune des cartes du jeu qui ont toutes un fonctionnement différent. Les cartes du jeu sont regroupées en plusieurs catégories, les cartes action, les cartes victoire, les cartes trains, les cartes rails. Nous avons donc créé une classe carte puis des classes abstraites pour chacun des types de cartes. Ensuite, chacune des cartes implémente l'interface qui lui correspond. Ce qui nous donne l'architecture suivante (seules quelques cartes ont été représenté sur le diagramme):

![diagramme de classes des cartes](/images/Diagrammes-classes-cartes.png)

Il a fallu ensuite coder le tour d'un joueur pour qu'il puisse jouer une carte qu'il a en main, acheter une carte de la réserve seulement s'il a l'argent nécessaire. En clair toutes les actions possibles pour un joueur, mais également programmer la fin de partie le décompte des points et l'affichage du classement final. Pour gérer les scores et gérer les cartes rails, nous avons dû appréhender le plateau de jeu fourni dans le squelette de code initial.

Tout au long du projet, nous avons vérifié le bon fonctionnement des fonctionnalités du jeu notamment des cartes grâce à des tests unitaires. Mon camarade a créé un nombre conséquent de tests unitaires ce qui nous a permis de s'assurer du bon déroulement de notre jeu.

## Théorème des graphes

Dans un deuxième temps, nous avons pu, au travers de notre jeu, aborder un théorème mathématique très important en informatique : le théorème des graphes. 

En effet, le plateau de jeu est composé de plusieurs rangée de cases hexagonales. Chacun d'entre elles peut être considéré comme un sommet, et ces cases sont reliées si elles contiennent un jeton rail. Une fois ce principe énoncé, nous pouvons appliquer tout un tas de théorèmes et de propriétés propre au graphe. 

Nous avons donc créé une classe Sommet puis une classe Graphe composé d'une liste de sommets. Nous avons ensuite implémenté quelques algorithmes basiques comme "estUnCycle" ou "estUneChaine" qui renvoie vrai si le graphe est respectivement un cycle ou une chaîne. Puis, à l'aide de ces petites fonctions nous avons pu développer des algorithmes plus complexe comme l'algorithme des plus proches voisins ou l'algorithme des 3 couleurs.

## L'interface graphique 

La dernière étape de ce projet a été de développer notre propre interface graphique. Nous avons développé cette interface avec java fx.
Cette interface comporte un plateau de jeu, une réserve de carte, une interface joueur ainsi que des règles de jeu facilement accessible.
Comme une image vaut mieux que mille mots, vous pouvez consulter la version final du projet sur mon github.

![Interface graphique Trains](/images/Trains.png)