---
layout: post
title: PHP - assert()
date: 2023-09-01
author: NZ0H
categories: [Root-Me, Web-Serveur]
tags: [Root-Me, Web-Serveur, PHP-assert()]
---

# PHP - assert()
## Défi
Objectif : Trouver et exploiter la vulnérabilité pour lire le fichier .passwd.

### Etape 1

L'objectif est tout d'abord d'analyser la page sur laquelle nous arrivons.

![Capture d'écran de la page d'accueil](/assets/Images/ROOT-ME/Web%20-%20Serveur/PHP%20-%20assert()/c1.png)

Nous pouvons voir une page simple, sans informations, à part une petite blague du créateur du défi :
***"You will never find out where our secrets are located... ahahaha (Evil laugh)"***

### Etape 2

Nous pouvons remarquer qu'il y a une barre de navigation avec les options **"*Home*"**, **"*About*"**, **"*Contact*"**. Allons voir où elles mènent.

Voici le contenu de la page ***Home*** :
![Capture d'écran de la page Home](/assets/Images/ROOT-ME/Web%20-%20Serveur/PHP%20-%20assert()/c2.png)

Voici le contenu de la page ***About*** :
![Capture d'écran de la page About](/assets/Images/ROOT-ME/Web%20-%20Serveur/PHP%20-%20assert()/c3.png)

Voici le contenu de la page ***Contact*** :
![Capture d'écran de la page Contact](/assets/Images/ROOT-ME/Web%20-%20Serveur/PHP%20-%20assert()/c4.png)

Seulement du contenu textuel qui change, rien de plus.

### Etape 3

Le nom du défi est "assert()", et **assert()** est souvent utilisé par les développeurs pour obtenir le retour de leur code avec les erreurs pour les corriger.

Essayons d'exécuter du code dans l'URL, nous verrons bien...

![Capture d'écran de l'exécution de code dans l'URL](/assets/Images/ROOT-ME/Web%20-%20Serveur/PHP%20-%20assert()/c5.png)

Nous pouvons voir que la requête fonctionne bien et que nous pouvons exécuter des commandes. Par exemple, la commande liste les fichiers du répertoire avec les permissions et diverses informations.

Mais notre objectif est d'afficher le flag. Comment faire ? Nous pouvons voir que dans le retour de la commande **ls -al**, il y a le fichier .passwd avec une permission de lecture :

![Capture d'écran du fichier .passwd](/assets/Images/ROOT-ME/Web%20-%20Serveur/PHP%20-%20assert()/c6.png)

Pourquoi ne pas essayer la commande **'.system("cat .passwd").'** et regarder son résultat ?

![Capture d'écran de la commande cat .passwd](/assets/Images/ROOT-ME/Web%20-%20Serveur/PHP%20-%20assert()/c7.png)
