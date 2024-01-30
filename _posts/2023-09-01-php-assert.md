---
layout: post
title: PHP - assert()
date: 2023-09-01
author: NZ0H
categories: [Root-Me, Web-Serveur]
tags: [Root-Me, Web-Serveur, PHP-assert()]
---

### Etape 1

L'objectif est tout d'abord d'analyser la page sur laquelle nous arrivons.

![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c1.png)


Nous pouvons voir une page simple, sans informations, à part une petite blague du créateur du défi :
***"You will never find out where our secrets are located... ahahaha (Evil laugh)"***

### Etape 2

Nous pouvons remarquer qu'il y a une barre de navigation avec les options **"*Home*"**, **"*About*"** , **"*Contact*"**. Allons voir où elles mènent.



Voici le contenu de la page ***Home*** : 
![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c2.png)

Voici le contenu de la page ***About*** : 
![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c3.png)

Voici le contenu de la page ***Contact*** :
![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c4.png)


Seulement du contenu textuel qui change, rien de plus.

### Etape 3

Le nom du défi est "Assert()", et **assert()** est souvent utilisé par les développeurs pour obtenir le retour de leur code avec les erreurs pour les corriger.

Essayons d'exécuter du code dans l'URL, nous verrons bien...

![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c5.png)


Nous pouvons voir que la requête fonctionne bien et que nous pouvons exécuter des commandes. Par exemple, la commande liste les fichiers du répertoire avec les permissions et diverses informations.

Mais notre objectif est d'afficher le flag. Comment faire ? Nous pouvons voir que dans le retour de la commande **ls -al**, il y a le fichier .passwd avec une permission de lecture :

![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c6.png)

Pourquoi pas essayer la commande **'.system("cat .passwd").'** et regarder son résulat ?

![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c7.png)


Et voilà, le flag est affiché sur la page !

