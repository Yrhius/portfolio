+++
title = 'Projet: ETCD_like'
description = "conception et réalisation d'un système distribué de clés/valeurs"
type = "post"
date = 2025-10-01
tags = ["système", "git", "c", "multithreads", "réseau"]
showTableOfContents = true
+++


Ce projet a été réalisé dans le cadre d'un cours de système de 3e année de BUT. Il a été conçu par 4 étudiant de l'IUT de Montpellier.

Ce projet met en place un système distribué de clé valeur, avec plusieurs nœuds serveur qui communiquent entre eux, stockent les données et communiquent avec le client qui souhaite ajouter, enlever ou lire des valeurs présente dans le sysème. Ce projet est divisé en trois étapes distinctes :
- le principe de communication de base entre les nœuds (ping-pong)
- le principe d'élection d'un leader parmi les nœuds (principe raft)
- le principe de communication avec le client et de gestion du dictionnaire clé/valeur

Ce programme est encore en cours d'évolution et malheureusement certaines features ne sont pas encore opérationnelles.

## STEP 1

Cette étape met en place le principe de communication de base entre les nœuds (ping-pong). Chaque noeud essaye de communiquer avec tous les autres, une fois que chacun a envoyé un ping et reçu un pong de chaque autres noeuds, ils se mettent en attente.

### Architecture 

![Architecture step1](/images/etcd-1-archi.png)

Sur l'image ci-dessus, vous pouvez voir la structure de cette première étape. Nous avons le pdf de consignes, un makefile pour compiler correctement notre projet, un fichier nodes.conf et divers dossiers. Le fichier nodes.conf contient les informations des noeux (id, adresse, port), nous en avons mis que trois le temps du développement de l'application mais l'on peut facilement augmenter leur nombre en ajoutant des lignes dans ce fichier.

Le dossier src contient les fichier de code:
- rpc.c, contient toute la logique de communication / réseau
- node.c, contient les fonctions pour lire le fichier nodes.conf
- main.c, lance les noeuds en multithreads et appelle les fonctions des deux autres fichiers

Le dossier include contient les headers(.h) des fichier de code (.c); le dossier build contient les fichiers compilés (.o) et target contient le fichier final regroupant tous les fichiers compilés du dossier build.

### Demonstration

![Demo step1](/images/etcd-1-output.png)

Déroulement du programme:

Node 0 est lancé, il lit le fichier nodes.conf et remarque qu'il y 3 nodes (lui compris). Il tente de se connecter au deux autres en vain.  
Node 1 est lancé, il lit aussi le fichier nodes.conf, node 0 arrive à le contacter. Les deux nodes s'envoient ping/pong et s'enregistrent comme étant en ligne Toutefois node 0 est toujours hors ligne.
Node 2 est lancé, il lit aussi le fichier nodes.conf et reçoit les pings des deux autres nodes. Il leur répond et les note comme en ligne.  
Ils sont tous en ligne et restent en attente.  

Les affichages peuvent être confus à cause des threads.



## STEP 2

Cette étape met en place le principe d'élection d'un leader parmi les nœuds (principe raft). Au bout de quelques milisecondes sans leader, un noeud va lancer une élection pour être leader. Lorsqu'un noeud reçoit une demande de vote, il compare sa version et celle du candidat. Si le candidat est en avance alors il vote pour lui. Quand un noued a reçu la majorité des votes il devient leader et prévient les autres noeuds qu'il est le nouveau master.

### Architecture 

![Architecture step2](/images/etcd-2-archi.png)

Sur l'image ci-dessus, vous pouvez voir la structure de cette deuxième étape. Il n'y a eu aucun changement de structure particulier sur cette étape. Le fichier config.c a été fusionné avec le fichier node.c.
Le code de main rpc et node a évolué pour mettre en place le système d'élection.


### Demonstration

![Demo step2](/images/etcd-2-output.png)

Déroulement du programme:

Node 0 est lancé, il attend.  
Node 1 est lancé, il attend.  
Lorsque le timeout sans leader de Node 0 est passé, il lance une élection et vote pour lui même. Il demande à Node 1 de voter pour lui et tente de demander à Node 2 en vain.   
Node 1 n'a pas commencé d'election de son coté alors il vote pour Node 0.  
Node 0 est élu leader 2 votes sur 3 et envoie un message aux autres noeuds pour leur dire. Il essaye en boucle de contacter node 2 sans succès.  
Node 2 est lancé, il reçoit l'information de Node 0. Node 2 n'a donc pas besoin de voter car il a déjà un leader.   
Node 0 arrête d'envoyer des paquets à Node 2.  
Tous les nodes sont prêts et connectés entre eux.  

![Demo suite step2](/images/etcd-2-output2.png)


Voici ce qu'il se passe si le leader est tué:

Node 0 est déconnecté.  
Le timeout de Node 1 est dépassé, il lance une élection et vote pour lui.  
Node 2 reçoit la demande de vote, il vote pour node 1 qui est en avance sur lui.  
Node 1 est élu leader il tente de contacter en en vain node 0.  
Node 0 se reconnecte il reçoit l'information du leader.  
Node 1 arrête l'envoie de messages.  

Le système est de nouveau opérationnel


## STEP 3

Cette étape met en place le principe de communication avec le client et de gestion du dictionnaire clé/valeur. Le client va envoyer des requêtes à un noeud. Le noeud leader peut répondre à toutes les demandes, mais les noeuds follower ne peuvent que répondre aux requêtes get. Si le client interroge un follower pour entrer une valeur, le noeud lui dit alors qui est le leader et le client renvoie sa demande au leader cette fois. 

### Architecture 

![Architecture step3](/images/etcd-3-archi.png)

Sur l'image ci-dessus, vous pouvez voir la structure de cette deuxième étape. Certains fichiers ont été rajoutés pour répondre aux nouveaux besoins. Le fichier kvstore gère le principe de dictionnaire, il contient les fonctions qui peuvent créer un dictionnaire, le modifier et insérer des valeurs. Le fichier client contient la logique client qui va communiquer avec les noeuds des requêtes GET et PUT.


### Demonstration

![Demo step3](/images/etcd-3-output.png)

Déroulement du programme:

Les noeuds sont lancés un par un et procèdent à l'élection du leader comme à l'étape 2.  
Le client fait une requête à un noeud pour entrer la valeur 10 pour la clé a.  
Par chance, sur l'image ci-dessus il contact le leader du premier cout. Le leader enregistre la valeur.
S'il avait interrogé un follower il aurait reçu un message lui indiquant qu'il n'a pas intérrogé le leader puis il aurait reçu le message lui disant que sa requête a bien été transmise au leader.  
Le client fait une requête à un noeud pour entrer la valeur toto pour la clé b. Le leader enregistre la valeur.

Malheureusement la fonction GET rencontre actuellement un problème et n'a pas pu être corrigé pour le moment par manque de temps.

## Conclusion

Ce projet m'a beaucoup apporté, il m'a permis de retravailler des concepts clé tels que le multithreads et les sockets en C. J'ai aussi découvert un principe bien plus grand que je connaissais pas du tout, celui des systèmes distribués. J'ai compris qu'ils étaient très présents dans notre monde aujourd'hui : cryptomonnaie, blockchain, etcd ... Et j'ai également réalisé toute la complexité d'un tel système. Enfin, j'ai continué d'approfondir mes compétences en C que je développe depuis la première année de BUT.