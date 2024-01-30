---
layout: post
title: TCP - Retour au collège
date: 2023-09-01
author: NZ0H
categories: [Root-Me, Programmation]
tags: [Root-Me, Programmation, TCP]
---

```python
# Importation des différentes bibliothèques utilisées
import socket
import struct
import math
import re

# Initialisation des paramètres de connexion
HOTE = 'challenge01.root-me.org'
PORT = 52002

# Création de la socket
soc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Connexion au serveur
soc.connect((HOTE, PORT))
print("Vous êtes bien connecté au serveur.\n")

# Réception des données envoyées par le serveur
receive = soc.recv(1024).decode()

# Récupération des valeurs dans le texte envoyé : n1 -> 2 (pour les deux secondes)
# n2 et n3 sont les valeurs générées aléatoirement par le serveur
n1, n2, n3 = re.findall(r'\d+', receive)

# Initialisation du calcul dans une variable, racine de n1 * n2
# Résultat sous forme d'une chaîne de caractères et le résultat est arrondi à 2 chiffres après la virgule
value = str(round((math.sqrt(int(n2))) * (int(n3)), 2))

# Envoi du calcul au serveur
soc.send(value.encode())
soc.send(receive.encode())
reponse = soc.recv(1024).decode()

# Affichage de la réponse
print(reponse)

# Fermeture de la connexion au serveur
soc.close()
```