+++
title = "5. Projet: Site de Vente en Php"
+++

## Introduction

Lors de ma formation, j'ai eu la chance de créer mon propre site web dynamique à l'aide de Php. Avec deux autres camarades, j'ai imaginé et conçu un site de vente en ligne de sweats. Le site a une partie back-end avec une base de données contenant les informations des marchandises et une partie front-end qui gère l'affichage dynamique des informations.

## Une base de donnée

La base de données est composé de 6 tables:

Taille: Contient les différentes tailles possible avec le sigle et la description (XL, très grand)  
Sweat: Contient un code, un nom, une couleur et un prix  
Utilisateur: Contient toutes les infos utiles de l'utilisateur tel que login, nom, prenom, mot de passe haché, etc  
Stock: Indique pour un sweat et une taille donnée le nombre d'article disponible  
Commande: Associe un numéro de commande à une date et à un utilisateur  
Lignecommande: Contient un sweat, une taille et une quantite d'une ligne d'une commande

![Modele E/A](/images/BDD_E-A_Php.png)  

Les interactions avec la BD sont gérées par le php. Le site permet aux administrateurs de gérer les stocks, en ajoutant de nouvelles taille de nouveau sweat et en augmenter le stock d'un sweat donné avec une taille donnée, mais également de gérer les utilisateurs. Coté utilisateur, on peut ajouter des sweats à notre panier et passer commande ce qui diminue les stocks en BD.

Les requêtes vers la BD sont donc variées. La majorité des informations des requêtes sont reçues via des formulaires html et envoyer à travers des requêtes post, puis le fichier php adéquat créé une requête l'envoie à la BD. Une fois que le BD à envoyé sa réponse php la traite et gère l'affichage, mais nous parlerons de ce point après. 
Nous avons tenu à avoir un site sécurisé au maximum ce qui implique de protéger notre base de données.

Premièrement, les mots de passe des utilisateurs sont haché grâce au protocole sha256 et stocké chiffré dans la bdd ce qui assure la confidentialité des informations de nos clients.

![fonction de hashage](/images/Mdp_Hash_Php.png) 

Deuxièmement, notre site est protégé face aux injections sql. En effet, notre script php fait des requêtes préparées et utilise des fonctions pour échapper les caractères spéciaux html, php et sql.

![requetes préparées](/images/Requete_Preparee_Php.png) 

## L'affichage 

Grâce au php, les informations de la BD sont traité et utilisé afin de produire un affichage ergonomique. Nous avons choisi un css épuré et propre pour ne pas surcharger de couleurs. Chaque sweat est affiché avec une image permettant de visualiser le produit. 

Voici quelques images du site web:

La page des sweats: 

![page sweats](/images/Affichage_Site_Php.png) 

Les infos d'un sweat et le formulaire d'ajout au panier:

![page détail sweat](/images/Affichage_Ajout_Php.png) 

Le formulaire de création d'un compte:

![page création de compte](/images/Affichage_Formulaire_Php.png) 