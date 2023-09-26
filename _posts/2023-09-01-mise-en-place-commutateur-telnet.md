---
layout: post
title: Telnet sur commutateur
date: 2023-09-01
author: NZ0H
categories: [Cours, Cours Réseau]
tags: [Cours, Commutateur,Telnet]
---

Configuration d'une authentification telnet :

```bash
Switch> enable
Switch# configure terminal
Switch(config)# username 'identifiant' secret 'mot de passe'
Switch(config)# line vty 0 4
Switch(config-line)# transport input telnet
Switch(config-line)# login local
Switch(config-line)# exit
Switch(config)# end
```

Telnet est un protocole peu fiable, les échanges ne sont pas chiffré (donc vulnérable à l'attaque Man In The Middle).