+++
title = 'Projet: La base de données de Spotify'
description = "conception et réalisation d'une base de donnée capable de contenir des information extraites de spotify"
type = "post"
date = 2024-03-01
tags = ["BDD", "Modélisation", "math"]
showTableOfContents = true
+++

Vous êtes-vous déjà demandé à quoi ressemble la base de données d'une grande entreprise mondiale ? Nous oui ! 

Lors de ma première année de BUT informatique à Montpellier, j'ai eu l'occasion de creuser cette question à travers le cas de spotify. En effet, nous avons reçu plusieurs fichiers Excel contenant des milliers d'information provenant de la base de données de Spotify ou plus exactement des fausse donnée qui pourrait venir de cette entreprise. Avec l'aide de trois autres camarades, nous avons imaginé et conçu une base de données permettant de contenir ces données de la façon la plus optimisée. Nous avons ensuite inséré les données, écrit une succession de requêtes pour récolter des informations sur cette masse donnée. Enfin, nous avons exploité les données récupérées par nos requêtes pour faire diverses statistiques sur Spotify et ses utilisateurs. 

## Analyse et Conception 

Avant de se lancer dans la création de la base de données, il nous fallait trouver comment relier les informations entre elles, quelle serait la structure de notre base de données. Pour cela, nous avons fait un brainstorming important puis nous avons créé un modèle Entité/Association plutôt satisfaisant. Des petites modifications ont ensuite été apportées lors du développement.

Les informations présentes dans les fichiers étaient de types très variés. De fait, Spotify gère des musique, des artistes et des utilisateurs qui ont tous, plusieurs informations, qui leurs sont propre. Par exemple, un utilisateur a un identifiant, un pseudo, un genre, une date de naissance, mais on connaît également le dernier morceau qu'il a écouté et où il s'est arrêté dans cette musique. Il peut être un utilisateur premium, avoir des playlists, des dossiers, suivre des artistes, avoir des amis sur l'application, bloquer d'autre utilisateur et encore bien d'autres choses. Au final, nous avions pas moins de 28 tables différentes dont plus d'un quart ont plus de 4 colonnes. Voici le modèle EA de notre BDD :

![Modele EA](/images/ModeleEA.png)   

## Développement

Une fois la conception terminée, nous avons créé la base de données. Le script de création de table fait plusieurs centaines de lignes de code, soit pas moins de 8 pages de Google doc ! Le développement de la BDD était assez facile, un seul problème subsister la gestion des playlist et des dossiers. Ce problème est assez connu et peut être résolu grâce au pattern décorateur du Gang of Four (GOF) que j'ai pu apprendre plus tard. Cependant, au moment du projet je ne connaissais aucun paterne du GOF, ce petit problème m'a donc donné du fil à retordre mais j'ai fini par trouver la solution, sans même le savoir je venais d'utiliser mon premier pattern du GOF. 

L'insertion des données n'a pas été évidente non plus. Les tableurs comprenaient pour certains des milliers de lignes, il nous aurait fallu des heures pour insérer toutes les données une par une. Pour remédier à cela, nous avons utilisé Debeaver et nous avons créé des vues temporaire, grâce à l'application la transformation des fichier Excel en vue sql était facile et rapide. Il nous fallait ensuite insérer les données dans nos tables depuis nos vues matérielles. Bien que ce procédé réduise le temps et le nombre de ligne de code, l'insertion des données comprend pas moins de 5 pages.

## Statistiques

Nous avons ensuite pu écrire quelques requêtes intéressantes plus ou moins compliquées pour extraites des informations sur notre BDD. Nous avons pu récupérer toutes les informations concernant chacun des morceaux, les morceaux les plus écoutés par un utilisateur ou encore la note médiane des notes des morceaux.

Grâce à ces informations, nous avons pu faire les graphiques suivants :

![Modele EA](/images/Histogramme_sorties.png)   

![Modele EA](/images/Proportion_albums.png)   
