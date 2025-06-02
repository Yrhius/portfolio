+++
title = '4. Projet: Une application de vote'
+++

## Introduction

De nos jours, la communication interne aux entreprises est primordiale. Nous le remarquons notamment via tous les logiciels de communications qui fluctuent sur le marché (Workplace, Jamespot, Zoom..). En tant que chef d’entreprise, réussir à collecter des informations pour pouvoir s’organiser est un des principaux piliers pour faire fonctionner son entreprise efficacement. Dès lors, les différentes manières de récupérer ces informations méritent un certain approfondissement.
Bien que ces moyens de communication soient nombreux et diversifiés, ils sont aussi génériques et impersonnels car disponibles à tous. Il serait alors sensé que de vouloir une application créée spécialement pour soi, répondant précisément à nos exigences. C’est là le but de notre projet, créer une application de sondage anonyme selon des critères bien définis.
Notre projet permet donc de répondre au besoin de notre client. Celui-ci est un patron d’entreprise, il souhaite pouvoir récolter les avis de ses employés sur certaines questions/décisions importantes concernant l’entreprise. Il aimerait pour cela disposer d’une application permettant de gérer ses questions sous forme de votes cryptés et sécurisés. C’est pourquoi il a fait appel à notre équipe de développeurs.

## Developpement 

Notre projet s'est développé en plusieurs parties : l'analyse, la conception puis la production.


La première étape de notre projet consiste à se renseigner sur le milieu dans lequel notre projet se situe, d’un point vue légale ou bien marketing, savoir ce qu’il se fait déjà, ce qu’on peut faire. Mais il faut également bien cerner notre propre projet, être sur des attendus du client des contraintes qu’il nous impose, mais aussi des contraintes techniques que nous avons (nos outils, nos effectifs, nos connaissances).

Une fois l’analyse terminée, nous avions tous le projet en tête. Nous connaissions les fonctionnalités principales, mais également les petits détails importants à prendre en compte. Cependant, avant de commencer à développer de l’application, il nous fallait l’imaginer, concevoir son architecture et ses différentes parties. Durant cette phase de conception, nous nous sommes basées sur notre analyse de l’existant, mais également sur nos connaissances et notre expérience pour choisir la meilleure architecture possible.

Il apparaît vite que cette application se compose en réalité de deux applications distinctes : une cliente et un serveur. L’application serveur a besoin de communiquer avec les applications, mais également de communiquer avec une base de données. Tandis que l’application cliente a besoin de communiquer uniquement avec le serveur, mais elle a besoin d’une interface graphique pour les futurs utilisateurs de l’application. Nous avons longuement hésité à faire 3 types d’application cliente (scrutateur, électeur, administrateur), mais nous avons finalement opté pour une seule application cliente divisée en trois sous-parties.

![mon CV](/images/Interface_Admin.png)

La base de données nous est indispensable, elle permet de simplifier beaucoup de choses et de stocker de façon durable les diverses informations de notre application. En effet, la base de données permet de stocker les différents sondages, les différents utilisateurs et savoir qui a voté sur quel référendum. La table CLIENT contient les informations du client tel que son identifiant et son mot de passe crypté qui nous permet de vérifier l'identité d'un utilisateur à travers une page de connexion. Cette table nous permet également de savoir si le client est électeur, scrutateur ou administrateur. La table REFERENDUM recense les données des référendums ; leur identifiant, leur description (la question qui a été posée), la date de fin de vote, mais également le nombre de votes et le Résultat chiffré et celui déchiffré quand le référendum est fini.
Enfin une troisème table AVOTE permet de relier les deux table précédente et nous permet de savoir si le client 1 a voté au referendum A ou B, de sorte a ce qu'aucun électeur ne puisse répondre plusieurs fois au même sondage.

![mon CV](/images/Vote.png)

Le protocole de communication entre le serveur et le client est basé sur du TCP/IP. La connexion est aussi chiffrée de manière transparente avec du TLS pour plus de sécurité. Le serveur suit ces étapes :
Le serveur charge sa clé privée pour la connexion TLS
Le serveur comment à écouter les connexions entrantes
Lorsqu’un client se connecte, il envoie un ID de paquet qui correspond à une action que le client souhaite faire (voir un vote, faire un vote…).
Le client et le serveur échangent des données liées à l’action que le client souhaite faire (si le client veut voir un vote, il envoie l’identifiant du vote par exemple.). À ce moment-là, le serveur peut communiquer avec sa base de données si nécessaire.
Lorsque l’action est finie, la connexion est coupée. Si le client souhaite faire une autre action, alors il doit se reconnecter et renvoyer un paquet.
Il existe plusieurs types de paquets différents pour chaque action possible qu’un client puisse faire.

![mon CV](/images/Resultat.png)

Nous avons utilisé Thymeleaf avec Spring MVC pour une intégration cohérente entre le front et la logique métier.
Les entités principales sont :
Utilisateur : Acteurs interagissant avec le système (administrateur, scrutateur et électeurs).
Vote : Les votes avec lesquels les utilisateurs peuvent interagir.
Processus : 
Gestion des utilisateurs (inscription, authentification, modification mot de passe)
Votes (choisir un vote, électeurs en capacité de voter)
Gestion des votes (Création des votes, déchiffrage, envoie)
Règle d'interaction : 
Administrateur : Gestion utilisateur, création de votes
Scrutateur : Gestion du chiffrement des votes
Électeur : Se contente de choisir un référendum et de voter


## Gestion de projet 

Afin d’organiser notre travail, nous avons choisi d’adopter la méthode agile pour contrôler le flux de travail de notre projet. Nous avons constitué une équipe avec un Product Owner (désormais PO), un Scrum Master et trois développeurs. Le PO, responsable de la vision du produit et de la gestion du backlog, a régulièrement communiqué avec le client, ce qui nous a permis de garder une charge de travail relativement maîtrisée durant les différents sprints.

Quelques dates importantes:
Début septembre: lancement du projet
24/09/24: premier échange avec le client, marque la fin du sprint 0 et le début du sprint 1
16/10/24: rendu de sprint 1, marque le début du sprint 2
12/11/24: rendu de sprint 2, marque le début du sprint 3
9/12/24: rendu de sprint 3, marque le début du sprint 4, le sprint final
09/01/25: livraison du projet 


Nous avons utilisé GitLab pour notre prochain. Nous avons créé les User stories sous forme d’Issues que nous avons pu attribuer à chacun et trier selon des labels comme l’état de la user story, sur quoi elle porte, son effort, etc. Nous avons pu créer différentes branches, afin de séparer notre travail et de pouvoir travailler sur plusieurs Users stories en même temps sans se gêner les uns les autres. Voici différentes branches qui ont été créées au cours du projet.

De manière générale, une branche est créée à chaque nouvelle user story. Une fois une fonctionnalité terminée, une merge request est faite. Le Scrum Master(SM) et le Product Owner vérifient le code produit et valide la requête si tout va bien. Par exemple : Alexis a modifié le code de l’application serveur afin de respecter les principes SOLID. Pour cela, il a créé une branche, il a ensuite travaillé dessus en effectuant des commits réguliers. Une fois son travail fini, il crée une merge request et l’assigne à Samuel le SM. Samuel se connecte un peu plus tard, étudie le code produit et valide la merge request. Lors d’un push, grâce à la CI, la pipeline est exécutée nous permettant de voir facilement si le code qui va être merge est viable ou non.

En parallèle, nous avons utilisé google drive, afin de partager au sein du groupe de nombreux documents. Nous avons notamment rédigé des traces de communication, pour chaque sprint nous avons un fichier contenant les différentes traces des daily meeting ainsi que de la rétrospective de sprint. Nous avons également les documents de prise de notes lors des entretiens avec le client et un document comportant l’ensemble des questions que nous avons eu besoin de poser à ce dernier.

## Conclusion

Ce projet m'a permis d'apprendre beaucoup de choses et d'approfondir mes connaissances. D’une part, j'ai renforcé nmes connaissances en java, sql ou encore en html. D’une autre part, j'ai appris de nouvelles technologies et framework : l’utilisation de Spring pour gérer une interface graphique, l’utilisation de jdbc pour interagir avec une base de données dans une application java ou encore l’utilisation des Sockets en java sans oublier docker. Ce projet a également été l’occasion de mettre en pratique des connaissances vu uniquement en cours. En effet, j'ai pu mettre en pratique dans un cas concret mes compétences SOLID et certains patterns de GOF. 

La méthode agile m'a permis de découvrir une nouvelle façon de travailler. Elle nous a permis de garder une direction et un suivi de projet cohérent avec les attentes du client. En effet, le principe des sprints et de suivi continu nous permet de garder une communication régulière et concise. De plus, en tant que Scrum Master, j'ai joué un rôle majeur dans la communication de l'équipe. J'ai favorisé les échanges entre les membres du groupe et j'ai essayé d'instaurer le plus possible un climat propice à l'épanouissement de chacun au sein de notre équipe.

N'hésitez pas à consulter notre rapport de projet pour en apprendre davantage.

[Rapport de projet](https://docs.google.com/document/d/1hyIf02A4aEvFCnX3DevLNIpdkuVqPVxGG6C9iTvt1c4/edit?usp=sharing)   