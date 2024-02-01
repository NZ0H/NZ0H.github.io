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

---
layout: post
title: Bluetooth - Fichier inconnu
date: 2023-10-19
author: NZ0H
categories: [Root-Me, Réseau]
tags: [Root-Me, Réseau, Bluetooth]
---

# Bluetooth - Fichier inconnu
## Défi

Objectif :
Votre ami travaillant à l’ANSSI a récupéré un fichier illisible dans l’ordinateur d’un hacker. Tout ce qu’il sait est que cela provient d’un échange entre un ordinateur et un téléphone. À vous d’en apprendre le plus possible sur ce téléphone.
La réponse est le hash SHA1 de la concaténation de l’adresse MAC (en majuscules) et du nom du téléphone.

Voici la trame que nous obtenons quand nous l’ouvrons avec Wireshark : 

![Image](/assets/Images/ROOT-ME/Reseau/bluetooth/c1.png)

Wireshark comporte de nombreux filtres dont un filtre permettant d’obtenir des informations sur les équipements durant un échange Bluetooth (Wireless > Équipements Bluetooth) : 
![Image](/assets/Images/ROOT-ME/Reseau/bluetooth/c2.png)

Nous pouvons observer l’adresse MAC mais aussi le nom du téléphone. 

À présent, nous devons concaténer le résultat et générer un SHA1 à partir de cette concaténation : 

![Image](/assets/Images/ROOT-ME/Reseau/bluetooth/c3.png)

