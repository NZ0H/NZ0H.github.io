---
layout: post
title: TCP - Chaîne encodée
date: 2023-09-01
author: NZ0H
categories: [Root-Me, Programmation]
tags: [Root-Me, Programmation, TCP]
---

```python
# Importation des différentes bibliothèques utilisées
import socket 
import codecs 

# Initialisation des paramètres de connexion
HÔTE = 'challenge01.root-me.org'
PORT = 52021

# Création de la socket
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Connexion au serveur
sock.connect((HÔTE, PORT))
print("Vous êtes bien connecté au serveur.\n")

# Réception des données envoyées par le serveur
receive = sock.recv(1024).decode()
v = receive.split("'")

reponse = codecs.decode(v[1], 'rot_13')

# Envoi des caractères décodés
sock.send(reponse.encode())
sock.send(receive.encode())

flag = sock.recv(1024).decode()

# Affichage du flag
print(flag)

# Fermeture de la connexion au serveur
sock.close()
```