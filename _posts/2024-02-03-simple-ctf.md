---
layout: post
title: Simple CTF
date: 2024-02-03
author: NZ0H
categories: [Try Hack Me,CTF-Simple]
tags: [THM,CTF]
---

# Simple CTF
## Défi

![image](/assets/Images/THM/Simple-CTF/c1.png)

### Combien de services fonctionnent sur le port 1000 ?

Pour afficher le nombre de services qui fonctionne entre le port 1 et le port 1000, nous pouvons utiliser une commande `nmap`.

![image](/assets/Images/THM/Simple-CTF/c2.png)

Nous pouvons observer deux services actifs, le service **ftp** et **http** :

![image](/assets/Images/THM/Simple-CTF/c3.png)

### Qu'est-ce qui s'exécute sur le port supérieur ?

Grâce à la commande **nmap** effectuée ci-dessus, on peut voir que sur le port 2222, c'est le service ssh qui est exécuté.

![image](/assets/Images/THM/Simple-CTF/c4.png)

### Quel est le CVE que vous utilisez contre l'application ?

CVE : **`CVE (Common Vulnerabilities and Exposures) permet de recenser toutes les failles et les menaces liées à la sécurité des systèmes d'informatique.`**

Actuellement, nous n'avons pas assez d'informations sur la machine pour déterminer une vunérabilité. Cependant, nous avons vu 3 services qui étaient actifs, dont le service **http**, ce qui peut indiquer la présence d'un site web. Pour avoir plus d'informations, nous allons faire une énumération sur l'adresse **http://10.10.218.32/** avec DirBuster.

Pendant que l'énumération continue à se faire, j'utilise les premières informations retournées par dirbuster pour ne pas perdre de temps :

![image](/assets/Images/THM/Simple-CTF/c5.png)

Voici la page principale du site :

![image](/assets/Images/THM/Simple-CTF/c6.png)

Dessus, nous obtenons des informations sur l'entreprise, comme le fait qu'elle fournisse un service de générateur de site web, d'où le nom CMS (Content Management System) made simple. Dans le bas de page, nous pouvons obtenir la version du CMS :

![image](/assets/Images/THM/Simple-CTF/c7.png)

Avec un nom de service et une version, nous pouvons commencer à essayer de recueillir des informations pour voir si une faille est repertoriée. Pour cela, nous allons utiliser **Metasploit** :

![image](/assets/Images/THM/Simple-CTF/c8.png)

On peut voir une liste d'exploitation de failles. Dans notre cas, CMS Made Simple est en version 2.2.8, ce qui veut dire que la technique utilisée pour exploiter la faille est une injection SQL.

Pour obtenir le numéro CVE, nous allons utiliser le site [ExploitDB](https://www.exploit-db.com/)

![image](/assets/Images/THM/Simple-CTF/c9.png)


Essayons de saisir ce numéro de CVE :

![image](/assets/Images/THM/Simple-CTF/c10.png)

### À quel type de vulnérabilité l'application est-elle vulnérable ?

Comme nous avons pu le voir ci-dessus et comme l'a confirmé le numéro de CVE, l'application est vulnérable aux injections SQL.

![image](/assets/Images/THM/Simple-CTF/c11.png)

### Quel est le mot de passe ?
En cherchant le numéro de CVE, nous avons obtenu un script permettant d'exploiter la vulnérabilité CMS Simple Made. Nous allons donc utiliser ce script est voir les informations qu'il nous retourne grâce à la commande `python3 /home/malwabrut/cve-2019-9053\ .py -u http://10.10.218.32/simple/ --crack -w /usr/share/` :

![image](/assets/Images/THM/Simple-CTF/c12.png)

![image](/assets/Images/THM/Simple-CTF/c13.png)

### Où pouvez-vous vous connecter avec les détails obtenus ?

Au début du challenge, nous avons fait un scan qui nous montre qu'un service ssh est actif. Nous allons essayer une connexion ssh. Si cela ne marche pas, nous chercherons un autre type de connexion.

![image](/assets/Images/THM/Simple-CTF/c14.png)

![image](/assets/Images/THM/Simple-CTF/c15.png)

### Quel est le drapeau de l'utilisateur ?

Maintenant que nous sommes connectés au compte utilisateur, nous listons le répertoire pour commencer une prise d'information :

![image](/assets/Images/THM/Simple-CTF/c16.png)

Nous trouvons un fichier **cat.txt**, qui nous permet de trouver le flag demandé.

![image](/assets/Images/THM/Simple-CTF/c17.png)

### Y a-t-il un autre utilisateur dans le répertoire personnel ? Quel est son nom ?

Après cela, nous listons le répertoire ***/home*** pour avoir la liste des utilisateurs. Nous trouvons un autre nouvel utilisateur '**sunbath**'.
![image](/assets/Images/THM/Simple-CTF/c18.png)

![image](/assets/Images/THM/Simple-CTF/c19.png)

### Que pouvez-vous faire pour créer un shell privilégié ?

Pour effectuer une élévation de privilèges, plusieurs méthodes sont disponibles. Dans notre cas, nous allons examiner les permissions **sudo** qui nous sont accordées.

![image](/assets/Images/THM/Simple-CTF/c20.png)

Nous constatons que le compte actuel a le droit d'utiliser les privilèges **sudo** avec la commande **vim**.

![image](/assets/Images/THM/Simple-CTF/c21.png)

### Quel est le drapeau root ?

L'objectif est de détourner la commande ***sudo vim*** pour s'attribuer les privilèges **root**. Nous utilisons le site **GTFOBins**, spécialisé dans le contournement des restrictions de droits sur les sessions locales.

![image](/assets/Images/THM/Simple-CTF/c22.png)

Nous testons la première commande '**vim -c ':!/bin/sh'**'. La commande fonctionne bien et nous permet de récupérer le dernier flag.

![image](/assets/Images/THM/Simple-CTF/c23.png)

![image](/assets/Images/THM/Simple-CTF/c24.png)