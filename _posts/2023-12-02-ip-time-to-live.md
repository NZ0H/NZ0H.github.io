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
Le TTL est la duré de vie d'un paquet IP, chaque fois qu'un routeur transfet le paquet, il décrémente le TTL de 1. Lorsque le TTL atteint zéro, le paquet est supprimé.
Le TTL fait parti de la couche IP.
```
## Défi
Objectif : Retrouvez le TTL employé pour atteindre l’hote ciblé par cet échange de paquets ICMP.

Voici le début de la capture :
![image](/assets/Images/ROOT-ME/Reseau/ip-ttl/c1.png)

Nous pouvons voir qu’un hôte cherche à ping une cible mais malheureusement c’est un échec. Dans ce défi l’objectif est de trouver le paquet qui montrera que l’hôte a pu contacter sa cible.

Nous allons commencer par utiliser un filtre Wireshark qui retournera les requêtes ICMP ayant eu une réponse positive : 
![image](/assets/Images/ROOT-ME/Reseau/ip-ttl/c2.png)


Nous voyons que le numéro 72 est le premier paquet ayant réussi à retourner une réponse. Nous pouvons aussi voir que la requête vient du paquet numéro 71 (request in 71), voici donc le paquet 71.

![image](/assets/Images/ROOT-ME/Reseau/ip-ttl/c3.png)


Comme il a été dit dans la définition du TTL au début du compte rendu, le TTL fait partie de la couche IP, nous pouvons donc voir que le champ TTL a une valeur de 13 dans la couche 3.