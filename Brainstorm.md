# Description générale du projet 

Ce projet vise à avoir un endroit pour gérer tout l'aspect écologique et énergétique d'un logement. 
L'intérêt est de pouvoir y connecter tous les équipement connectés 


# Description technologique

## Description générale
Le projet vise à être relié à un home assistant. 

L'objectif du projet est de fournir les livrables suivants : 
1. Un serveur local pour la collecte des données des différents endpoints et serveurs distant
2. Une tablette avec une application mobile ou web visant à manager le logement.
    a. Une interface admin pour la gestion du logement vistant à automatiser des processus, gérer certains réglage ou autre
    b. Une interface data visant à analyser le logement sur le long terme, évaluer de potentiels changements, prédire des données, etc..

## Le serveur local 
Le serveur local sera déployé en C# ASP.NET testé sous un environnement docker.
Dans l'idéee, on viserait une utilisation avec api.home-management.local et le serveur agirais aussi comme un DNS sur le réseau wifi local. 

Le serveur local à plusieurs objectifs : 
1. Récupération des données : 
    a. Données des équipements connectés : prise connectée, climatisation connectée, etc..
    b. Données de serveurs externes : équipement connecté mais disponnible qu'à travers l'API du fournisseur; Fournisseur d'éléctricité, de Gas ou autre. 
2. Interagir avec les équipements connectés : Allumer/Eteindre des lumières, alumer/éteindre la climatisation ou chauffage, redirection de l'electricité vers/depuis les batteries, etc...
3. Traiter les données et fournir une api pour la gestion des données
4. Faire office de support pour la mise à jour du site ou de la partie interface (tablette) c'est à lui d'aller chercher les mises à jours depuis internet

## L'interface (tablette)

Aujourd'hui, je n'ai pas décidé entre une application lourde ou une application web.
Ce qui est sûr est que l'interface ne doit pas communiquer avec internet, techniquement, le système doit pouvoir fonctionner en duo local sans internet.

Je vois l'affichage de la manière suivante : 
1. L'interface admin : 
    a. Des écrans orienté "exploitation", un terme référant à la gestion au quotidien du logement. En soit, quelques écrans "Dashboard" avec la consomation actuelle d'électricité, de gaz, d'eau, la température, l'humidité, etc.., les équipements connectés, les alertes, etc..
    b. Des écrans orienté "configuration", la liste et configuration des équipements connectés, leurs IP, protocoles, etc... 
    c. Des écrans de gestion : l'idée est de gérer ici le paramétrage, "On alume la climatisation lorsque l'intérieur du logement est au dessus de 33° et on la met à 29°C" ou "Si le système est en mode vacance, on désactive la climatisation, les équipement connectés et le chauffe-eau jusqu'à la veille du retour prévu". C'est l'écran où l'on va créer l'ensemble des règles de gestion du système.
2. L'interface data : 
    a. Ecrans pour chaque système connecté, sa consomation énergétique depuis qu'il a été relié.
    b. Ecrans sur l'optimisation ou non des règles de gestion : par exemple, se rendre compte que couper la climatisation durant la journée où on est pas là, puis la remttre à l'arrivée, c'est moins efficace que la laisser toute la journée. Que le chauffage consome X€ par an, etc.. 
    c. Export de données sur tout
    d. Prédiction des consomations future

### Discussion au sujet d'une interface lourde 

Je suis fervant défenseur de l'optimisation des systèmes et permettre une utilisation minimale sur les machines. Cela permettant ainsi d'avoir une tablette qui a une gestion de la batterie accrue, et pouvoir avoir la tablette accrochée à un mur pendant une semaine sans nécessité de la recharger, et ainsi l'avoir à portée de main facilement. 
Cela permettrait aussi d'affiner l'utilisation pour des tablettes très bas de gamme, voire même avec des écrans e-inc.

### Discussion au sujet d'une interface web

D'un autre côté, une interface web, une simplicité d'écriture, pouvoir avoir accès depuis le téléphone, le PC et la tablette sans avoir à faire 3 applications. Cela aussi permettant d'accélérer le développement et de profiter des nombreuses librairies open-source. 