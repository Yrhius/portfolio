+++
title = 'Projet: Rustic, une solution de sauvegarde'
description = "conception et réalisation d'une solution de sauvegarde sécurisé en rust"
type = "post"
date = 2025-11-01
tags = ["rust", "système", "git", "sécurité", "crypto", "réseau"]
showTableOfContents = true
+++


## Une solution de sauvegarde à notre façon

Lors de mon cours de cybersécurité, on a vu l’importance de sauvegarder ses données afin d’être prêt à toute éventualité et pouvoir facilement relancer son SI après une attaque même si nos données ont été bloquées. Grâce à un système de sauvegarde efficace et régulier, le risque de perdre ses données devient minime.

C’est pourquoi nous avons lancé ce projet, afin de créer notre propre solution de sauvegarde. Je me suis regroupé avec trois autres camarades pour s’entraider.

Lien du projet https://github.com/Rustic-Backup/Rustic-IUT

### Analyse et conception

Nous avons décidé d’analyser ce qu’il se fait déjà afin de s’en inspirer. Nous avons ensuite tiré une liste de caractéristiques que nous souhaitions mettre dans notre programme. Voici une liste de features que nous souhaitions mettre en place :
 - pouvoir sauvegarder sur un serveur distant
 - pouvoir chiffrer les sauvegardes
 - pouvoir garder plusieurs versions d’une sauvegarde
 - pouvoir vérifier l’état de notre sauvegarde
 - pouvoir lister toutes nos sauvegardes
 - pouvoir avoir des informations sur nos sauvegardes(taille, date, compression etc)

Lors de nos recherches, un camarade est tombé sur la solution de sauvegarde Restic. Leur solution nous a beaucoup plus bien qu’un peu trop complexe pour notre utilisation. Nous avons donc décidé de garder une partie de l’architecture du code, mais en le simplifiant et en l’implémentant en Rust.

### Documentation 

Rustic dispose des différentes commandes suivantes:
 - backup: permet de sauvegarder les fichiers d’un dépôt
 - check: vérifie l’intégrité d’une sauvegarde 
 - help: permet d’avoir des informations sur les diverses commandes et sur leur syntaxe
 - init: permet de créer un dépôt pour pouvoir effectuer des sauvegardes
 - list: permet de lister toutes nos sauvegardes  
 - prune: permet de supprimer une ou plusieurs sauvegardes  
 - restore: permet de récupérer une sauvegarde
 - stats: affiche des informations sur une sauvegarde ou sur l’ensemble de nos sauvegardes


Rustic comporte une cli documentée, toutefois, pour plus d’information vous pouvez vous référer au readme du projet.

![Rustic cli](/images/rustic-cli.png)  

### Architecture du projet

![Rustic architecture](/images/rustic-archi.png)  

Vous pouvez voir ci-dessus, les différents fichiers de code du projet. 

Le fichier **cli.rs**, gère l'affichage graphique dans le terminal. Il permet d'interpréter les entrées dans le terminal et d'afficher des message d'erreur ou de la documentation, si les entrées sont invalides.  

Le fichier **main.rs** est le coeur de notre projet, il reçoit les commandes venant de la cli et lance les fonctions adéquat. Ce fichier effectuer tout le setup de base de l'application.  

Les fichier **backup.rs**, **restore.rs** et **stats.rs** gère respectivement la logique des commandes backup, restore et stat. Ces commandes nécessitant beaucoup de lignes de code elles ont été mis dans des fichiers séparés pour ne pas surcharger le main. 

Le fichier **config.rs**, gère la création et la lecture des fichier de configuration utiliser dans les dépots de sauvegardes.  

Le fichier **error.rs**, nous permet de générer différents type d'erreur ainsi que des messages adaptés au problème. Certaines message d'erreur sont la uniquement en cas de problème pour nous aider à debug et d'autres sont la pour informer l'utilisateur.  

Le fichier **lib.rs** permet à nos fichiers de codes de pouvoir utiliser les fonctions des autres fichiers.  

Le fichier **network.rs** gère la communication réseau de l'application, notamment la connection ssh à un serveur distant de sauvegarde.  

Le fichier **repository.rs** est un point clé du projet, il contient tout la logique des dépots de sauvegarde, il va de paire avec le fichier versioning.rs.  
Enfin le fichier versioning.rs gère les sauvegarde en elle même, et la possibilité d'avoir plusieurs versions d'une sauvegarde.  



## Conclusion

Ce projet est amené à évoluer dans le temps. Il m’a permis d’apprendre le Rust qui est un langage de plus en plus utilisé. J’ai également réalisé la complexité des logiciels de sauvegarde et l’importance d’effectuer des sauvegardes régulièrement. Ce projet m’a beaucoup plus, je l’ai trouvé particulièrement intéressant, car nous avons réellement conçu une solution qui pourrait être utilisée dans le monde professionnel.
