---
layout: post
title: FTP-Authentification
date: 2023-12-02
author: NZ0H
categories: [Root-Me, Réseau]
tags: [Root-Me, Réseau,FTP]
---
# FTP - Authentification
## Qu'est ce que FTP ?
```
FTP (File Transfert Protocol) est un service permettant le transfert de fichier via Internet.
```

## Partie challenge 

Objectif : Un échange authentifié de fichier réalisé grâce au protocole FTP. Retrouvez le mot de passe utilisé par l’utilisateur.

Voici la capture : 
![image](/assets/Images/ROOT-ME/Reseau/ftp-auth/c1.png)


10.20.144.150 est le poste client et 10.20.144.151 est le serveur, sur les trois première ligne on voit un échange permettant de dire qu'il y a l'établissement d'une conenxion. La partie qui nous intéresse est de la ligne 8 à la ligne 13 : 
![ftp](/assets/Images/ROOT-ME/Reseau/ftp-auth/c2.png)

L'utilisateur renseigne l'identifiant et le mot de passe, à la ligne 13 on peut observer que la connexion a bien était établie grâce à 'logged on'.