---
layout: post
title: PHP - assert()
date: 2023-09-01
author: NZ0H
categories: [Root-Me, Web-Serveur]
tags: [Root-Me, Web-Serveur, PHP-assert()]
---

### Etape 1

L'objectif est premierement d'analyser la page sur laquel on apparait.

![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c1.png)


On peut voir une page simple, sans information à part une petite blague du créateur du défie :
***"You will never find out where our secrets are located... ahahaha (Evil laugh)"***

### Etape 2

On peut voir qu'il y a une barre de navigation avec **"*Home*"**, **"*About*"** , **"*Contact*"**, allons voir où cela mène.

Voici le contenu de la page ***Home*** : 
![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c2.png)

Voici le contenu de la page ***About*** : 
![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c3.png)

Voici le contenu de la page ***Contact*** :
![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c4.png)


Seulement du contenue textuelle qui change, rien de plus.

### Etape 3

Le nom du défie est "Assert()", **assert()** est souvent utilisé par les développeur, cela permet d'avoir le retour de leur code avec les erreurs pour corriger.

Essayons d'executer du code dans l'url nous verrons bien ... 

![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c5.png)


On peut voir que la requete fonctionne bien et que nous pouvons éjéctuer des commande, par exemple la commande liste les fichiers du répertoire avec les permissions et diverse informations.

mais notre objectif est d'afficher le flag, comment faire ....
On peut voir que dans le retour de la commande **ls -al**, il y a le fichier .passwd avec une permission de lecture : 

![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c6.png)

Pourquoi pas essayer la commande **'.system("cat .passwd").'** est regarder son résulat ??

![](/assets/Images/ROOT-ME/Web - Serveur/PHP - assert()/c7.png)


BINGO le flag est affiché sur la page !

