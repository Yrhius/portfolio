+++
title = 'Alternance au sein de le DSI du CINES'
description = "description de mon alternance de 3eme année"
type = "post"
date = 2025-09-01
tags = ["système", "réseau", "sécurité"]
showTableOfContents = true
+++



## Introduction


Le BUT informatique permet d’effectuer sa troisième année en alternance, c’est une opportunité incroyable qui nous permet d’en apprendre plus sur le monde du travail et de mettre à profit nos apprentissages. J’ai la chance d’avoir réussi à trouver une alternance auprès du CINES (Centre Informatique National d’Enseignements Supérieurs).



![Cines logo](/images/cines-logo.jpg) 



Le CINES à trois grande missions : 
le Calcul Intensif : Des moyens exceptionnels à la disposition des chercheurs pour relever de grands défis scientifiques.
l’Archivage: Une solution performante pour la conservation à long terme du patrimoine numérique des établissements
l’Hébergement: L’expérience du CINES dans l’exploitation des environnements informatiques et la mutualisation de ses infrastructures exceptionnelles permettent d’accueillir dans ses salles machines les serveurs stratégiques de partenaires nationaux

Si vous souhaitez en savoir plus sur le CINES: https://www.cines.fr/

Mon alternance s’effectue au sein de la DSI, en tant que technicien système et réseau. Je suis là pour aider mes collègues à gérer les nouvelles demandes, à appliquer les changements nécessaires pour respecter les nouvelles normes ou encore assurer le maintien en conditions opérationnelles des solutions existantes.


## Déployer LemonLDAP



![Logo lemonldap](/images/cines-lemonldap.png) 



Ma première mission au sein du CINES consiste à déployer et à tester la solution lemonldap afin de s’assurer qu'elle réponde à nos besoins.

En effet, le CINES à de nombreuses contraintes à respecter en tant qu’établissement public, mais aussi dû au fait qu’il héberge des données de santé et des données militaires. C’est pourquoi l’architecture réseau doit être modifiée et il est nécessaire de changer la répartition des services pour respecter la nouvelle architecture. Ces changements interviennent également au niveau du LDAP.

Avant mon arrivée, le projet a été lancé et la solution lemonldap a été évoquée comme étant une solution capable de remplir les critères du nouvel LDAP. J’ai donc commencé mon alternance par me renseigner sur cette solution et l’installer manuellement sur une machine dédiée. Bien que je ne connaissais pas du tout ce service, je n’ai pas eu trop de problèmes avec l’installation manuelle, car il existe beaucoup de documentation à ce sujet.

J’ai ensuite dû retranscrire toutes les étapes d’installation dans la forge Ansible. Cette partie a été bien plus longue pour diverses raisons. Tout d’abord, je ne connaissais pas du tout Ansible. J’ai donc lu beaucoup de documentation et regardé diverses vidéos afin de comprendre l’utilité de Ansible, comment il fonctionne et comment l’utiliser. Ensuite, le CINES utilise Ansible depuis longtemps, et cumule beaucoup de rôles et de playbook. L’infrastructure existante est conséquente et il m’a fallu du temps pour m’y habituer. Enfin, après avoir assimilé les concepts de base d’Ansible et avoir appris l’infrastructure du CINES, il fallait que j’améliore mes connaissances en YAML.

Une fois l’installation faîte, il faut tester de connecter diverses applications à lemonldap afin de s’assurer que tout fonctionne comme prévu. Cette partie est encore en cours de réalisation.


## Conclusion

Je suis très heureux d’évoluer au sein du CINES. Cet établissement possède des outils informatiques de qualité ainsi que des informaticiens compétents qui sont tous bienveillants et enclins à m’aider quand j’en ai besoin. Je suis certain que les mois à venir seront encore très instructifs et intéressants.
