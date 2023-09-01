---
layout: post
title: OSPF-Authentification
date: 2023-09-01
author: NZ0H
categories: [Root-Me, Réseau]
tags: [Root-Me, Réseau, OSPF-Authentification]
---
### Etape 1 :

On ouvre la capture Wireshark : 

![](/assets/Images/ROOT-ME/Reseau/OSPF-Authentification/c1.png)

On peut voir que la capture a déjà était filtré, il y a que le protocole OSPF, allons voir un des paquets.

### Etape 2 : 

L'objectif est de trouver le champ OSPF dans le paquet, et de trouver diverse information sur l'authentification.

![](/assets/Images/ROOT-ME/Reseau/OSPF-Authentification/c2.png)

Auth Type -> 2 signifie que le mot de passe est sous la forme d'un hash, 1 correspond au mot de passe affiché clairement. 
Auth Crypt Key id -> la clef porte l'id 10 sur le routeur.
Auth Crypt Data Length -> 16 nous permet de savoir que c'est un chiffrement MD5.
Auth Crypt Sequence Number -> Le numéro de la séquence d'échange.
Auth Cypt Data -> On peut voir le hash de la clef.

### Etape 3 : 

Maintenant que l'on à compris les champs du paquet, nous allons récupérer les informations : 

![](/assets/Images/ROOT-ME/Reseau/OSPF-Authentification/c3.png)



ettercap nous permet de traiter des paquets réseaux, -T affiche sous la form d'un texte, -q quitetr après finit le traitant, -r permet de chercher les différents mots de pas ou empreinte dans la capture.

### Etape 4 : 

On ajoute le résultat de la commande précédente dans un fichier sous cette forme : 

![](/assets/Images/ROOT-ME/Reseau/OSPF-Authentification/c4.png) 

Maintenant plus qu'à casser le hash ! Pour cela on va utiliser john avec une des wordlists les plus connues, rockyou.txt.

![](/assets/Images/ROOT-ME/Reseau/OSPF-Authentification/c5.png)

Voici le flag !