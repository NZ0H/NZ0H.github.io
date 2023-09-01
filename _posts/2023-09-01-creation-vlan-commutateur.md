---
layout: post
title: VLAN sur commutateur
date: 2023-09-01
author: NZ0H
categories: [Cours, Cours Réseau]
tags: [Cours, Commutateur, VLAN]
---

Nous allons créer 3 vlans : 

| Vlan     | Interfaces | Adresse IP   |
| -------- | ---------- | ------------ |
| vlan 2   | Fa0/0-9    | 192.168.2.1  |
| vlan 3   | Fa0/10-19  | 192.168.3.1  |
| vlan 7   | Fa0/20-24  | 192.168.7.1  |

```bash

// Attribution des privileges
Switch> enable
Switch# configure terminal

// Création des vlans
Switch(config)# vlan 2
Switch(config-vlan)# name VLAN2

Switch(config)# vlan 3
Switch(config-vlan)# name VLAN3

Switch(config)# vlan 7
Switch(config-vlan)# name VLAN7

// Configuration IP des interfaces des vlans
Switch(config)# interface vlan 2
Switch(config-if)# ip address 192.168.2.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

Switch(config)# interface vlan 3
Switch(config-if)# ip address 192.168.3.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

Switch(config)# interface vlan 7
Switch(config-if)# ip address 192.168.7.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

// Attribution des interfaces aux vlans
Switch(config)# interface range FastEthernet0/0 - 9
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 2
Switch(config-if-range)# no shutdown
Switch(config-if-range)# exit

Switch(config)# interface range FastEthernet0/10 - 19
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 3
Switch(config-if-range)# no shutdown
Switch(config-if-range)# exit

Switch(config)# interface range FastEthernet0/20 - 24
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 7
Switch(config-if-range)# no shutdown
Switch(config-if-range)# exit

// Création d'un mode trunk sur l'interface Fa0/24
Switch(config)# interface FastEthernet0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk native vlan 7
Switch(config-if)# switchport trunk allowed vlan 7
Switch(config-if)# no shutdown
Switch(config-if)# exit

Switch(config)# end
```