+++
title = 'Mon Stage au Pole numérique et données de la ville de Montpellier'
description = "description de mon stage de 2eme année"
type = "post"
date = 2025-01-27
tags = ["système", "réseau", "sécurité", "supervision"]
showTableOfContents = true
+++

## Introduction:

Dans le cadre de ma formation, j’ai eu la chance de réaliser un stage au sein de la collectivité territoriale Montpellier Méditerranée Métropole. Ce stage a duré 8 semaines, du 3 février au 28 mars 2025, j’ai pu évoluer en tant que technicien réseaux et système. En effet, la ville de Montpellier dispose d’un Pôle Numérique et Données(PND) composé de diverses couches métiers allant de l'application au réseau en passant par la télécom, le système, et la sécurité. Elle a développé au fil des années un réseau de plus en plus important. L’ensemble des sites publics de la ville sont équipés d’appareils électroniques, et chaque agent utilise un ensemble de sites web, d'applications et d’équipements informatiques. Ce secteur évolue vite, il est donc nécessaire de maintenir les infrastructures, d’étendre le réseau à de nouveaux lieux et d’intervenir en cas d’incident.

![logo 3M](/images/Logo_3M.png)

Mon stage m’a permis de couvrir à la fois du réseau, du système, mais également un peu de sécurité en lien avec mon projet d’avenir. Le but étant de me permettre de découvrir beaucoup d’univers différents en mettant en pratique mes connaissances et d'apporter mon aide sur les différentes missions prévues en février et en mars. 

Pour la partie réseau, j’ai participé à la maintenance du réseau informatique et à la résolution de problèmes. J’ai également aidé au déploiement de nouveaux équipements informatiques sur les nouveaux sites gérés par la collectivité. Pour la partie système, j’ai été chargé de mettre en place la supervision des sites internet et d’écrire une documentation permettant à l’équipe de reprendre mon travail à l’avenir.

Pour des raisons de sécurité et de confidentialité, le nombre de photos est limité et je ne peux dévoiler aucun détail technique. Merci de votre compréhension.

## Réseau

Le processus de mise en place de nouveaux switch dans une baie informatique est l'une des plus fréquentes que j’ai réalisé au sein de l’équipe réseau. J’ai eu l’occasion d’apprendre cette démarche pas à pas jusqu’à le faire de façon autonome. C’est une manipulation longue qui demande la compréhension de divers concepts. Voici les différentes étapes:

**Analyse des besoins et préparation:**

Étude des équipements existants : présence d’une baie, type et nombre de switchs en place, ports disponibles.  
Vérification des besoins spécifiques : nombre de nouveaux appareils, nécessité de switchs PoE (plus volumineux et bruyants).  
Exemple pratique : intervention pour les ASVP → remplacement de switchs obsolètes par un stack de deux switchs 48 ports PoE.  

![baie informatique avant](/images/ASVP_Avant.png)


**Étude du réseau et configuration initiale:**

Compréhension de l’architecture du réseau de Montpellier : structure pyramidale avec geo switch, fédérateurs, cœurs de réseau et sous-répartiteurs.   
Détermination de la plage IP, interfaces, VLAN et rôles (cœur de réseau, sous-répartiteur, etc.).   
Recherche d’informations via l’outil CORSE un outil interne au PND.   
Exemple : mise en place de VLAN pour caméras, postes pro, bornes Wi-Fi, management.   


**Préconfiguration des switchs en atelier**

Connexion via port console avec Putty.   
Création de stack (liaisons IRF, définition des priorités des membres).   
Chargement du fichier de configuration “master” (fichier de conf générique du PND) via GET, puis adaptation aux besoins spécifiques : nommage, interfaces, routes, VLAN, QoS, DHCP, chiffrement RSA, etc.   


**Installation sur site**

Vérification des lieux et de la baie, souvent désordonnée.   
Placement des nouveaux switchs, sans couper l’accès réseau immédiatement.   
Débranchement et retrait des anciens switchs, branchement du nouveau stack au réseau (via fibre).   
Brassage des câbles RJ45 de façon logique et propre.   
Configuration finale des ports spéciaux avec le câble console.  


**Vérifications et validation**

Test des voyants, des connexions réseau dans les salles, fonctionnement du Wi-Fi, imprimantes, badgeuses.   
Contrôle d’accès SSH et tests de communication réseau (ping).   
Vérification via l’outil de supervision Zabbix : disparition des alertes une fois les nouveaux switchs opérationnels.   

![baie informatique après](/images/ASVP_Apres.png)


## Système:

Ma mission a été de superviser des sites web et applications web au travers de leurs URL et de rédiger une documentation adaptée.





Mon but a donc été de mettre en place une supervision automatisée des sites web via Zabbix afin de détecter rapidement toute anomalie ou indisponibilité de service. Le principe de fonctionnement est le suivant:
J’utilise Zabbix pour effectuer des tests toutes les minutes.


**Méthodes de vérification :**

Code HTTP (ex. : 200 pour OK, 302 pour redirection).   
Présence d’une chaîne de caractères dans le code source.   
En cas d’échec : alerte immédiate via déclencheur Zabbix.   


**Procédure de configuration :**

Créer un groupe d’hôtes pour les sites à superviser.   
Ajouter deux hôtes par site : un pour l’environnement de production, un pour l’environnement de test.   


**Définir un scénario web par site :**


Sites sans login : 1 étape (URL + code HTTP attendu).   
Sites avec login : 3 étapes :   
Page de login (HTTP 200)   
Page d’authentification (identifiants)   
Page post-login (HTTP 200 ou texte attendu)   



**Limitations rencontrées:**

Protocole NTLM ou Kerberos :   
Authentification via pop-up système (non HTML).   
Impossible de détecter les champs "login" / "mot de passe".   
Stockage des identifiants en clair nécessaire → risque de sécurité.   



**Décision prise:**

Pas de supervision applicative sur les sites sensibles avec NTLM/Kerberos.   
Supervision uniquement du serveur hôte, pour détecter les pannes système.   


**Validation de la configuration:**

Vérification dans l’onglet Déclencheurs : tous doivent être "OK".   
Test manuel : modifier une étape volontairement pour vérifier l’alerte.   
Débogage dans l’onglet Web : étape défaillante, erreur HTTP, contenu manquant.   



**Documentation :**

Rédaction d’un guide interne comportant les étapes de configuration, les types de supervision possibles et les problèmes fréquents avec leur solutions



**Bonnes pratiques:**

Préférer un compte dédié à la supervision, avec des droits limités.   
Tester chaque scénario manuellement avant validation finale.   
Documenter chaque configuration dans l’outil de suivi technique.   

## Conclusion

Ce stage a été une belle opportunité pour moi et je suis sincèrement très reconnaissant envers chacune des personnes qui m'a permis de connaître cette expérience. J’ai pu aider l’équipe réseau à maintenir les infrastructures en conditions opérationnelles. La métropole étant très grande, les interventions sont parfois nombreuses et ma présence a été la bienvenue. La supervision des switchs à laquelle j’ai participé sera encore utilisée bien après mon départ et il en va de même avec la supervision des URL que j’ai fait en grande partie seul. J’ai fourni une documentation détaillée accessible à toute l’équipe système. La supervision comporte 43 sites surveillés comprenant des sites de production et des sites de test. Il va de soi que les switchs que j’ai configurés et mis en place vont rester jusqu’à ce qu’ils deviennent à leur tour obsolètes.   
Si vous avez des questions concernant ce stage n'hésitez pas à me joindre pour en parler
