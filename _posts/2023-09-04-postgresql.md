---
layout: post
title: Cheat Sheet PostgreSQL
date: 2023-09-04
author: NZ0H
categories: [Cheat-Sheet, PostgreSQL]
tags: [Cheat-Sheet, SQL, PostgreSQL]
---


## Connexion

```sql
-- si nous sommes connectée en root nous pouvons nous connecter directement comme ça :
psql 

-- Pour se connecter en local :
psql -U <username> -d <database> -h <hostname>

psql --username=<username> --dbname=<database> --host=<hostname>
```
## Deconnexion

```sql
\q
```
## Manipulation	de base de donnée

### Selectioner données

### Condition
##### OR
```sql
-- Cette condition vérifie si l'une ou l'autre des conditions est vraie.
SELECT * FROM produits
WHERE categorie = 'Électronique' OR categorie = 'Vêtements';
```

##### AND
```sql
-- Cette condition vérifie si toutes les conditions sont vraies.
SELECT * FROM employes
WHERE age >= 30 AND departement = 'Ressources humaines';
```

##### >
```sql
-- Cette condition vérifie si une valeur est supérieure à une autre.
SELECT * FROM commandes
WHERE montant_total > 1000;
```

##### <
```sql
-- Cette condition vérifie si une valeur est inférieure à une autre.
SELECT * FROM produits
WHERE prix < 50;
```

##### <= ou =>
```sql
-- Cette condition vérifie si une valeur est inférieure ou égale à / supérieure ou égale à une autre.
SELECT * FROM etudiants
WHERE moyenne >= 10 OR moyenne <= 5;
```

### Jointure

##### Simple jointure
```sql
-- Les jointures permettent de combiner des données de plusieurs tables en fonction de certaines conditions.
SELECT commandes.commande_id, clients.nom
FROM commandes
INNER JOIN clients ON commandes.client_id = clients.client_id;
```

##### Double jointure
```sql
-- Dans cet exemple, nous effectuons une double jointure entre trois tables : table_1, table_2 et table_3.
-- Nous utilisons INNER JOIN pour ne récupérer que les lignes correspondantes dans toutes les tables.

SELECT table_1.colonne_1, table_2.colonne_2, table_3.colonne_3
FROM table_1
INNER JOIN table_2 ON table_1.id = table_2.id
INNER JOIN table_3 ON table_2.id = table_3.id;
```

##### Triple jointure
```sql
-- Dans cet exemple, nous effectuons une triple jointure entre quatre tables : table_1, table_2, table_3 et table_4.
-- Nous utilisons INNER JOIN pour ne récupérer que les lignes correspondantes dans toutes les tables.

SELECT table_1.colonne_1, table_2.colonne_2, table_3.colonne_3, table_4.colonne_4
FROM table_1
INNER JOIN table_2 ON table_1.id = table_2.id
INNER JOIN table_3 ON table_2.id = table_3.id
INNER JOIN table_4 ON table_3.id = table_4.id;
```
*Le principe est le même si il y a plus de jointure à faire...*

## Manipulation de table
### Créer une table
```sql
-- Créer une nouvelle table
CREATE TABLE nom_de_la_table (
    colonne1 type_de_données,
    colonne2 type_de_données,
    ...
);
```


### Modifier une table
#### Ajouter une colonne à une table
```sql
-- Ajouter une colonne à une table existante
ALTER TABLE nom_de_la_table
ADD nom_de_la_colonne type_de_données;
```

#### Supprimer une colonne d'une table
```sql
ALTER TABLE nom_de_la_table
DROP COLUMN nom_de_la_colonne;
```

#### Modifier le type de donnée d'une table
```sql
-- Modifier le type de données d'une colonne
ALTER TABLE nom_de_la_table
ALTER COLUMN nom_de_la_colonne TYPE nouveau_type_de_données;
```

#### Renommer une table
```sql
-- Renommer une table
ALTER TABLE nom_de_la_table
RENAME TO nouveau_nom_de_la_table;
```


### Supprimer une table
```sql
-- Supprimer une table
DROP TABLE nom_de_la_table;
```






## Permissions

Devenir utilisateur PostgreSQL, en cas d'erreurs de permission :

```sql
sudo su - postgres
psql
```

Accorder toutes les permissions sur la base de données :

```sql
GRANT ALL PRIVILEGES ON DATABASE <db_name> TO <user_name>;
```

Accorder les permissions de connexion à la base de données :

```sql
GRANT CONNECT ON DATABASE <db_name> TO <user_name>;
```

Accorder les permissions sur le schéma :

```sql
GRANT USAGE ON SCHEMA public TO <user_name>;
```

Accorder les permissions pour exécuter les fonctions :

```sql
GRANT EXECUTE ON ALL FUNCTIONS IN SCHEMA public TO <user_name>;
```

Accorder les permissions pour sélectionner, mettre à jour, insérer, supprimer sur toutes les tables :

```sql
GRANT SELECT, UPDATE, INSERT, DELETE ON ALL TABLES IN SCHEMA public TO <user_name>;
```

Accorder les permissions sur une table spécifique :

```sql
GRANT SELECT, UPDATE, INSERT ON <table_name> TO <user_name>;
```

Accorder les permissions de sélection sur toutes les tables dans le schéma public :

```sql
GRANT SELECT ON ALL TABLES IN SCHEMA public TO <user_name>;
```
