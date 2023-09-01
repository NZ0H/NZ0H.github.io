---
layout: post
title: SQL injection - Authentification
date: 2023-09-01
author: NZ0H
categories: [Root-Me, Web-Serveur]
tags: [Root-Me, Web-Serveur, SQL-Injection]
---

### Etape 1 : 

Voici à quoi ressemble la page de login pour l'admin : 
![](/assets/Images/ROOT-ME/Web - Serveur/SQL Injection - Authentification/c1.png)

On peut voir un champ de login ou potentiellement on pourrait mettre 'admin' et un champ password où l'on mettra le mot de passe

Etape 2 : 

Comem le dit le titre du défie, il y a une faille sql d'authentification sur la page, pour commencer on va faire l'un des tests les plus simple de faille sql : 

![](/assets/Images/ROOT-ME/Web - Serveur/SQL Injection - Authentification/c2.png)


Login : 'admin'

Password : "' or 1=1; -"

On peut voir que l'injection a marché, mais ! Nous sommes connectés au user1, pour remedier à cela nous allons modifier l'injection:

Etape 3 : 

Login : admin ';-
Password :  "Champ aléatoire .., MAIS OBLIGER DE METTRE QUELQUE CHOSE"

![](/assets/Images/ROOT-ME/Web - Serveur/SQL Injection - Authentification/c3.png)


BINGO nous sommes connectés au compte administrateur