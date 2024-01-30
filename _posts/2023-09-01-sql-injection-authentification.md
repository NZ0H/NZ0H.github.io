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

On peut voir un champ de login où potentiellement on pourrait mettre 'admin' et un champ de mot de passe où l'on mettra le mot de passe.

Etape 2 : 

Comme le titre du défi l'indique, il y a une faille SQL d'authentification sur la page. Pour commencer, nous allons effectuer l'un des tests les plus simples pour trouver la faille SQL :

![](/assets/Images/ROOT-ME/Web - Serveur/SQL Injection - Authentification/c2.png)


Login : 'admin'

Password : "' or 1=1; -"

On peut voir que l'injection a fonctionné, mais ! Nous sommes connectés en tant que user1. Pour remédier à cela, nous allons modifier l'injection.

Etape 3 : 

Login : admin ';-
Password :  "Champ aléatoire ..,  MAIS OBLIGÉ DE METTRE QUELQUE CHOSE"

![](/assets/Images/ROOT-ME/Web - Serveur/SQL Injection - Authentification/c3.png)


Et voilà, nous sommes connectés au compte administrateur