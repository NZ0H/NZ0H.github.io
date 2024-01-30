---
layout: post
title: Bluetooth-Fichier inconnu
date: 2023-10-19
author: NZ0H
categories: [Root-Me, Réseau]
tags: [Root-Me, Réseau,Bluetooth]
---
# Bluetooth - Fichier inconnu
## Défi

Objectif :
Votre ami travaillant à l’ANSSI a récupéré un fichier illisible dans l’ordi d’un hacker. Tout ce qu’il sait est que cela provient d’un échange entre un ordinateur et un téléphone. A vous d’en apprendre le plus possible sur ce téléphone.
La réponse est le hash SHA1 de la concaténation de l’adresse MAC (en majuscules) et du nom du téléphone.

Voici la trame que nous obtenons quand nous l'ouvrons avec Wireshark : 

![image](https://hackmd.io/_uploads/S1rlvPB9a.png)

Wireshark comporte de nombreux filtre dont un filtre permettant d'obtenir des informations sur les equipements durant un échange Bluetooth (Wireless > Equipements Bluetooth) : 
![image](https://hackmd.io/_uploads/SkZ2PPS96.png)

On peut observer l'adresse MAC mais aussi le nom du téléphone, à présent nous devons concaténer le résultat et génerer un SHA1 à partie de cette concaténation : 

![image](https://hackmd.io/_uploads/ryynuvrc6.png)

