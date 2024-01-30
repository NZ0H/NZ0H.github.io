---
layout: post
title: SQL injection - Authentification
date: 2023-09-01
author: NZ0H
categories: [Root-Me, Web-Serveur]
tags: [Root-Me, Web-Serveur, SQL-Injection]
---

# SQL injection - Authentification
## Défi
Objectif : Retrouver le mot de passe de l’administrateur.
### Etape 1 : 

Voici à quoi ressemble la page de login pour l'admin :
![Capture d'écran de la page de login](/assets/Images/ROOT-ME/Web%20-%20Serveur/SQL%20Injection%20-%20Authentification/c1.png)

On peut voir un champ de login où potentiellement on pourrait mettre 'admin' et un champ de mot de passe où l'on mettra le mot de passe.

### Etape 2 : 

Comme le titre du défi l'indique, il y a une faille SQL d'authentification sur la page. Pour commencer, nous allons effectuer l'un des tests les plus simples pour trouver la faille SQL :

![Capture d'écran de l'injection SQL](/assets/Images/ROOT-ME/Web%20-%20Serveur/SQL%20Injection%20-%20Authentification/c1.png)


Login : 'admin'

Password : "' or 1=1; -"

On peut voir que l'injection a fonctionné, mais ! Nous sommes connectés en tant que user1. Pour remédier à cela, nous allons modifier l'injection.

### Etape 3 : 

Login : admin ';-
Password : "Champ aléatoire ..,  MAIS OBLIGÉ DE METTRE QUELQUE CHOSE"

![Capture d'écran de l'injection modifiée](/assets/Images/ROOT-ME/Web%20-%20Serveur/SQL%20Injection%20-%20Authentification/c1.pngg)
