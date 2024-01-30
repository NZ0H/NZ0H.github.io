---
layout: post
title: ETHERNET-Trame
date: 2023-10-12
author: NZ0H
categories: [Root-Me, Réseau]
tags: [Root-Me, Réseau, Trame-Ethernet]
---

# ETHERNET - Trame
## Défi

Retrouvez les données normalement confidentielles contenues dans cette trame.

Pour cela, nous allons devoir reconstituer cette trame : 
![Image](/assets/Images/ROOT-ME/Reseau/ethernet-trame/c1.png)

Nous utiliserons un site web (https://hpd.gasmi.net/), il est aussi possible de le faire de manière manuscrite ou alors d'utiliser un langage de programmation.

![Image](/assets/Images/ROOT-ME/Reseau/ethernet-trame/c2.png)

Nous pouvons observer un champ 'HTTP', ce qui veut dire que les données transitent de manière claire. Voici le champ HTTP : 
![Image](/assets/Images/ROOT-ME/Reseau/ethernet-trame/c2.1.png)

Le champ '***Authorization***' contient les données envoyées au format base64, mais nous pouvons voir dans le champ '***Credentials***' les données décodées. Pour vérifier, nous allons décoder '***Y29uZmk6ZGVudGlhbA==***'.

![Image](/assets/Images/ROOT-ME/Reseau/ethernet-trame/c3.png)

On peut voir que le résultat est le même.
