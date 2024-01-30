---
layout: post
title: IP-Time To Live
date: 2023-12-02
author: NZ0H
categories: [Root-Me, Réseau]
tags: [Root-Me, Réseau,TTL]
---
# IP - Time To Live
## Qu'est ce qu'un TTl ?
```
Le TTL est la duré de vie d'un paquet IP, chaque fois qu'un routeur transfet le paquet, il décrémente le TTL de 1. Si le TTL atteint zéro, le paquet est supprimé.
Le TTL fait partit de la couche IP.
```
## Défi
Objectif : Retrouvez le TTL employé pour atteindre l’hote ciblé par cet échange de paquets ICMP.

Voici le début de la capture : 
![image](/assets/Images/ROOT-ME/Reseau/ip-ttl/c1.png)

On peut voir qu'un hôte cherche à ping une cible mais malheureusement c'est un échec. Dans ce défie l'objectif est de trouver le paquet qui montrera que l'hôte a pu contacter sa cible.

On va commencer par utiliser un filtre Wireshark qui retournera les requetes ICMP qui on eu une réponse positive : 
![image](/assets/Images/ROOT-ME/Reseau/ip-ttl/c2.png)


On voit que le numéro 72 est le premiere paquet ayant réussi à retourner une réponse. On voit aussi que la requete vient du paquet numéro 71 (request in 71), on va donc aller voir le paquet 71.

![image](/assets/Images/ROOT-ME/Reseau/ip-ttl/c3.png)


Comme il a était dit dans la définition du TTL au début du compte rendu, le TTL fait partie de la couche IP, on peut voir le champ TTL qui a une valeur de 13 (suffit plus cas mettre 13 en réponse).