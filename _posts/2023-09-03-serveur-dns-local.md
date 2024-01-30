---
layout: post
title: Montage d'un serveur DNS (local)
date: 2023-09-03
author: NZ0H
categories: [Cours, Mise en place de service]
tags: [Cours, DNS]
---

# DNS 
## Qu'est ce que le DNS
```
Le DNS est un service permettant 
```
## Mise en place d'un DNS avec bind9

### Mise en place de la zone direct
#### Configuration serveur  
Pour commencer nous allons installer le service Bind sur notre serveur : 

```sh
sudo apt update
sudo apt install bind9
```

En suite nous allons copier le fichier '*db.empty*' qui servira de modèle, pour ensuite créer notre configuration : 

```sh
cd /etc/bind
cp db.empty db.dns_malwabrut
``` 

A présent nous allons configurer le fichier '*db.dns_malwabrut*' : 

```bind
$TTL	86400
$ORIGIN dns.malwabrut.    ;  Variable contenant le nom de la zone pour permettre l’abréviation avec @

@	IN	SOA	dns.malwabrut.io. root.dns.malwabrut.io (
            20240127	; Serial
			 604800		; Refresh
			  86400		; Retry
			2419200		; Expire
			  86400 )	; Negative Cache TTL
;

@    IN    NS    dns.malwabrut.

;; debut des enregistrements DNS 
dns     IN    A    10.0.0.128
www     IN    A    10.0.0.127
;; fin des enregistrements DNS
```

Maintenant nous allons créer la zone 'dns.malwabrut', pour cela nous allons editer le fichier '*named.conf.local*' : 

```bind
zone "dns.malwabrut"{
    type master ;
    file /etc/bind/db.dns_malwabrut
};
```


#### Configuration Client

Pour tester notre serveur dns nous allons devoir ajouter l'adresse ip de notre serveur dns dans le fichier de configuration '/etc/resolv.conf' sur les postes clients : 

```shell
nameserver 10.0.0.128
```

Maintenant nous allons pouvour tester notre dns grâce à la résolution direct.

### Mise en place de la zone inverse

Nous allons copier le fichier '*db.dns_malwabrut*' pour gagner du temp sur notre configuration : 

```sh
cd /etc/bind
cp db.dns_malwabrut db.dns_malwabrut.inv
``` 

A présent nous allons configuratier le fichier '*db.dns_malwabrut.inv*' : 

```bind
$TTL	86400
$ORIGIN 0.0.10.in-addr.arpa.    ;  Variable contenant le nom de la zone pour permettre l’abréviation avec @

@	IN	SOA	dns.malwabrut.io. root.dns.malwabrut.io (
            20240127	; Serial
			 604800		; Refresh
			  86400		; Retry
			2419200		; Expire
			  86400 )	; Negative Cache TTL
;

@    IN    NS    dns.malwabrut.

;; debut des enregistrements DNS 
128    IN    PTR    @
;; fin des enregistrements DNS
```

Maintenant nous allons créer la zone inverse 'dns.malwabrut', pour cela nous allons editer le fichier '*named.conf.local*' : 

```bind
zone "0.0.10.in-addr.arpa"{
    type master ;
    file /etc/bind/db.dns_malwabrut.rev
};
```
Puis nous testons notre zone inverse avec les machines clientes

### Mise en place redirection DNS

La redirection DNS permettra de redirriger les requêtes DNS vers le serveur configuré dans le cas où notre serveur a pas la réponse à la requête DNS. Nous allons mettre le serveur DNS de Google comme serveur de redirection, il faut éditer le fichier 'named.conf.options' : 

```
options {
    forwarders {
        8.8.8.8;  
    };
    
};
```
