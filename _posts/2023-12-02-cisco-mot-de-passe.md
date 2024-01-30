---
layout: post
title: CISCO-Mot de passe
date: 2023-12-02
author: NZ0H
categories: [Root-Me, Réseau]
tags: [Root-Me, Réseau]
---
# CISCO - mot de passe
## Défi

Objectif : Trouvez le mot de passe "Enable".


Voici la configuration du routeur : 
```cisco
! Last configuration change at 13:41:43 CET Mon Jul 8 2013 by admin
! NVRAM config last updated at 11:15:05 CET Thu Jun 13 2013 by admin
!
version 12.2
no service pad
service password-encryption
!
isdn switch-type basic-5ess
!
hostname rmt-paris
!
security passwords min-length 8
no logging console
enable secret 5 $1$p8Y6$MCdRLBzuGlfOs9S.hXOp0.
!
username hub password 7 025017705B3907344E 
username admin privilege 15 password 7 10181A325528130F010D24
username guest password 7 124F163C42340B112F3830
!
!
ip ssh authentication-retries 5
ip ssh version 2
!
interface BRI0/0
 ip address 192.168.1.2 255.255.255.0
 no ip directed-broadcast
 encapsulation ppp
 dialer map ip 192.168.1.1 name hub broadcast 5772222
 dialer-group 1
 isdn switch-type basic-5ess
 ppp authentication chap callin
 no shutdown
!
!
interface GigabitEthernet1/15
 ip address 192.168.2.1 255.255.255.0
 no shutdown
!
router bgp 100
 no synchronization
 bgp log-neighbor-changes
 bgp dampening
 network 192.168.2.0 mask 255.255.255.0
 timers bgp 3 9
 redistribute connected
!
ip classless
ip route 0.0.0.0 0.0.0.0 192.168.1.1
!
!
access-list 101 permit ip any any
dialer-list 1 protocol ip list 101
!
no ip http server
no ip http secure-server
!
line con 0
 password 7 144101205C3B29242A3B3C3927
 session-timeout 600
line vty 0 4
 session-timeout 600
 authorization exec SSH
 transport input ssh
```

Grâce à la configuration on peut identifier cette ligne 'enable secret 5 $1$p8Y6$MCdRLBzuGlfOs9S.hXOp0.', où '$1$p8Y6$MCdRLBzuGlfOs9S.hXOp0.' est le hash MD5 cisco.

Pour commencer nous allons utiliser hashcat en faisant une attaque par dictionnaire pour trouver le mot de passe, via la commande '***hashcat -a 0 -m 500 hash.txt rockyou.txt***'.

Malheureusement, c'est un échec, le mot de passe n'est pas présent dans la liste, donc on pourrait faire une attaque par force brute. Etant un défi de cyber, les plateformes n'ont pas pour objectif de miser sur la puissance d'un ordinateur pour résoudre les défis, il doit y avoir une autre méthode.

On peut identifier 3 comptes sur le routeur : 
```cisco
username hub password 7 025017705B3907344E 
username admin privilege 15 password 7 10181A325528130F010D24
username guest password 7 124F163C42340B112F3830
```

Le chiffrement cisco de type 7 est extremement faible, on va donc utiliser un petit script python pour trouver les mots de passes. Notre objectif en faisant ça, est d'esperer que dans ce cas l'erreur vient de l'humain, et que le mot de passe soit le meme où alors donneun indice sur la structure du mot de passe.

Voici le script : 
```python
from passlib.hash import cisco_type7

hash_hub = '025017705B3907344E'
hash_admin = '10181A325528130F010D24'
hash_guest = '124F163C42340B112F3830'

password_hub = cisco_type7.decode(hash_hub)
password_admin = cisco_type7.decode(hash_admin)
password_guest = cisco_type7.decode(hash_guest)

print(f'Mot de passe du Hub : {password_hub}\nMot de passe du Admin : {password_admin}\nMot de passe du Gest : {password_guest}\n')
```

Le script retourne ce résultat : 
![image](https://hackmd.io/_uploads/r1JHGqS96.png)

On peut identifier un structure de mot de passe, ils commencent tous par '6sK0_' + le nom de compte. Alors essayons '6sK0_enable'(bonne réponse.




