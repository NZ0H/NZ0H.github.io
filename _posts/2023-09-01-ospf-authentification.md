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

![Capture d'écran Wireshark](/assets/Images/ROOT-ME/Reseau/OSPF-Authentification/c1.png)

On peut voir que la capture a déjà été filtrée, il n'y a que le protocole OSPF. Allons voir l'un des paquets.

### Etape 2 :

L'objectif est de trouver le champ OSPF dans le paquet et d'obtenir diverses informations sur l'authentification.

![Capture d'écran informations OSPF](/assets/Images/ROOT-ME/Reseau/OSPF-Authentification/c2.png)

Auth Type -> 2 signifie que le mot de passe est sous la forme d'un hash, 1 correspond au mot de passe affiché en clair.
Auth Crypt Key id -> la clé porte l'ID 10 sur le routeur.
Auth Crypt Data Length -> 16 nous permet de savoir que c'est un chiffrement MD5.
Auth Crypt Sequence Number -> Le numéro de la séquence d'échange.
Auth Crypt Data -> On peut voir le hash de la clé.

### Etape 3 :

Maintenant que nous avons étudié les différents champs du paquet, nous allons récupérer les informations :

![Capture d'écran informations récupérées](/assets/Images/ROOT-ME/Reseau/OSPF-Authentification/c3.png)

Ettercap nous permet de traiter les paquets réseau. -T affiche les données sous forme de texte, -q permet de quitter après avoir terminé le traitement, -r permet de rechercher les différents mots de passe ou empreintes dans la capture.

### Etape 4 :

On ajoute le résultat de la commande précédente dans un fichier sous cette forme :

![Capture d'écran ajout résultat dans un fichier](/assets/Images/ROOT-ME/Reseau/OSPF-Authentification/c4.png)

Maintenant, il ne reste plus qu'à casser le hash ! Pour cela, on va utiliser John avec l'une des wordlists les plus connues, rockyou.txt.

![Capture d'écran utilisation de JTR](/assets/Images/ROOT-ME/Reseau/OSPF-Authentification/c5.png)
