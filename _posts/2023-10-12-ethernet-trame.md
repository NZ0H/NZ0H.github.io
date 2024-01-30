---
layout: post
title: ETHERNET-Trame
date: 2023-10-12
author: NZ0H
categories: [Root-Me, Réseau]
tags: [Root-Me, Réseau,Trame-Ethernet]
---
# ETHERNET - trame
## Défi

Retrouvez les données normalement confidentielles contenues dans cette trame.


Pour cela nous allons devoir reconstituer cette trame : 
![image](https://hackmd.io/_uploads/SyL7TMNqp.png)

Nous utiliserons un site web (https://hpd.gasmi.net/), il est aussi possible de le faire de manière manuscrite où alors d'utiliser un language de programamtion.

![image](https://hackmd.io/_uploads/BJKyRMN5a.png)

Nous pouvons observer un champ 'HTTP', ce qui veut dire que les données transit de manière claire. Voici le champ HTTP : 
![image](https://hackmd.io/_uploads/BkHI0G456.png)

Le champ '***Authorization***' contient les données envoyées au format base64, mais nous pouvons voir dans le champ '***Credentials***' les données décodées. Pour vérifier nous allons décoder '***Y29uZmk6ZGVudGlhbA==***'.

![image](https://hackmd.io/_uploads/HyqmZXVcp.png)

On peut voir que le résultat est le même.