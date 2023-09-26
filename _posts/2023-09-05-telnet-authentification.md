---
layout: post
title: Telnet-Authentification
date: 2023-09-05
author: NZ0H
categories: [Root-Me, Réseau]
tags: [Root-Me, Réseau, Telnet-Authentification,Telnet]
---

On télécharge le défi, après avoir téléchargé le défi, nous l'onvrons avec Wireshark : 

![](/assets/Images/ROOT-ME/Reseau/TELNET-Authentification/c1.PNG)

Nous pouvons voir un échange Telnet qui a était capturé, le paquet transit grace au protocole TCP.

Wireshark a une option permettant de visualiser l'ensemble du trafic transporté via le protocole TCP, pour cela nous faisons un clique droit dans la console en bas: 

![](/assets/Images/ROOT-ME/Reseau/TELNET-Authentification/c2.PNG)

Voici le résultat : 

![](/assets/Images/ROOT-ME/Reseau/TELNET-Authentification/c2.PNG)

Nous avons trouvé le flag ! (ligne "Password")