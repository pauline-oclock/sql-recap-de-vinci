# Recap-SQL-blue

## Contraintes BDD

- Chaque ligne doit être unique
- Et possède un identifiant
- Pas de répétitions
- Pas de donnée calculée depuis un autre champ de la BDD

## Quelques requêtes 

- Connexion depuis le terminal: 
  - `mysql --user=root --password=root`

- Ne pas oublier, les requêtes se terminent par un `;`

- Afficher toutes les bases de données disponibles:
  - `SHOW DATABASES;`
- Utiliser une base de données:
  - `use nom_db;`
- Voir la liste des tables d'une base de données (nécessite d'être positionné sur une BDD)
  - `SHOW TABLES;`

- Sortir de l'invite de commande MySql: 
  - `exit;`

## Création d'une base de données

- AI: Auto increment => L'identifiant s'incrémente à chaque création de nouvelle ligne dans la table
  - En auto incrément, pas besoin de renseigner la valeur elle est automatisée
- Types de texte
  - VARCHAR : Texte limité à 255 caractères max, OBLIGATOIRE de définir la taille (lenght)
  - TEXT : Texte non limité en taille, pas besoin de définir sa taille MAIS prend beaucoup de place

## Clé primaire (PRIMARY KEY)

- La clé primaire est un élément unique qui identifie une ligne dans une table de la BDD
- Elle est indexée ce qui va permettre d'effectuer des liaisons entre tables plus efficacement ;) 

# SQL

## Commentaires

```sql
/*
Ceci est un commentaire
*/

-- Ceci est aussi un commentaire (Sur une seule ligne uniquement)
```

## Spécificités

- Pas de doubles quotes en SQL
- On encadre les chaînes de caractères par des simples quotes
- Les dates également
- On utilisera un seul = pour les conditions

## SELECT

- Permet d'afficher un retour
- On peut séparer les informations à afficher par des virgules
- On peut afficher par exemple des chaînes de caractère:
  - `SELECT 'Bonjour!', 'test';` 

## SELECT FROM

- Préciser où (sur quelle table) on va chercher les infos

```sql
-- SELECT : QUOI ?
SELECT name, editor
-- FROM : Où ?
FROM videogame;

-- * correspond à "TOUT"
SELECT *
FROM videogame;
```

### WHERE

- Préciser une condition pour la récupération des infos

```sql
-- SELECT : QUOI ?
SELECT name, editor
-- FROM : Où ?
FROM videogame
-- WHERE : Condition!
WHERE id=1;
```

- Conditions

```sql
-- égalité
WHERE id=1;
-- Supériorité 
WHERE id > 1;
-- Supériorité ou égalité
WHERE id >= 1;
-- Différence (!=)
WHERE id <> 1;
```

- AND et OR

```sql
SELECT name, editor FROM videogame WHERE id <> 1 AND editor = 'Konami';
SELECT name, editor FROM videogame WHERE id <> 1 OR editor = 'Konami';
```

## INSERT

```sql
-- On renseigne les informations dans l'ordre dans lequel les champs sont définis dans la table
INSERT INTO videogame VALUES(5, 'Final Fantasy X', 'Squaresoft', '2001-07-19', 4);

-- Si on ne renseigne pas l'ID (car auto incrementé), on doit le remplacer par NULL
INSERT INTO videogame VALUES(NULL, 'The Binding of Isaac', 'Edmund McMillen', '2011-07-28', 1);

-- On peut également préciser les champs qu'on va envoyer (tous les champs que vous voulez DANS LA MESURE Où ils SONT NULLABLES)
INSERT INTO videogame(name, platform_id) 
VALUES('Mortal Kombat', 2);
```

## UPDATE

- ATTENTION A BIEN DEFINIR UNE CONDITION POUR LA SUPPRESSION !!!

```sql
-- UPDATE: Modification
-- UPDATE table SET champ=nouvelle_valeur WHERE condition;
UPDATE videogame SET editor='Capcom' WHERE id= 7;
```

## DELETE

- ATTENTION A BIEN DEFINIR UNE CONDITION POUR LA SUPPRESSION !!!

```sql
DELETE FROM videogame WHERE id=7;
```

## SQL BONUS - LIKE

### _ Un caractère inconnu

```sql
-- LIKE : Qui ressemble à

-- _ = Remplace un et un seul caractère 
SELECT * FROM videogame WHERE name LIKE '___tlev_nia';
-- Résultat: Castlevania

-- Autre exemple avec _ pour chercher les jeux qui ont une longueur de 7 caractères
-- L'espace est considéré par MySql comme un caractère
SELECT * FROM videogame WHERE name LIKE '_______';
``` 

### % 0 ou plusieurs caractères

```sql
-- % = 0 ou +
-- Tous les jeux qui commencent par D
SELECT * FROM videogame WHERE name LIKE 'D%';

-- Tous les jeux qui finissent par c
SELECT * FROM videogame WHERE name LIKE '%c';

-- Tous les jeux qui contiennent la lettre y
SELECT * FROM videogame WHERE name LIKE '%y%';

-- Tous les jeux qui contiennent le terme of
SELECT * FROM videogame WHERE name LIKE '%of%';

-- Tous les jeux qui NE contiennent PAS le terme of
SELECT * FROM videogame WHERE name NOT LIKE '%of%';

```

## SQL BONUS - ORDER BY

```sql
-- ORDER BY : Ordonner PAR
-- ASC : Ascendant => De A à Z ou de 0 à 99+ [croissant]
-- DESC : Descendant => De Z à A ou de 99+ à 0 [décroissant]

-- Jeux dans l'ordre croissant de leur nom
SELECT * FROM videogame ORDER BY name ASC;

-- Jeux dans l'ordre décroissant de leur id
SELECT * FROM videogame ORDER BY id DESC;

-- Jeux dans l'ordre croissant de leur DATE !!
SELECT * FROM videogame ORDER BY release_date ASC;

-- Jeux par ordre croissant d'id de plateforme ET ordre croissant de nom d'éditeur
SELECT * FROM videogame ORDER BY platform_id ASC, editor ASC;
```

## SQL BONUS - LIMIT

```sql
-- LIMIT : Affiche un nombre max de lignes
SELECT * FROM videogame LIMIT 1;
SELECT * FROM videogame LIMIT 3;
SELECT * FROM videogame LIMIT 99;
```

## SQL BONUS - Count

```sql
-- COUNT : Compte le nombre de lignes retournées
SELECT count(id) FROM videogame;

SELECT count(id) FROM videogame WHERE platform_id = 1;
```

## SQL BONUS - Alias

```sql
-- AS 'nouveau nom' donne à la colonne le nom spécifié
SELECT count(id) AS 'Nombre' FROM videogame;
```

## IS NULL / IS NOT NULL

- Permet de vérifier si un élément est null

```sql
-- Vérifie si le champ image est NULL
SELECT * FROM author WHERE image IS NULL;
-- Vérifie l'inverse = le champ image n'est PAS NULL
SELECT * FROM author WHERE image IS NOT NULL;
```

## JOINTURE (JOIN / INNER JOIN)

Syntaxe:

```sql
SELECT champs
FROM table1 JOIN table2 
ON table1.champCorrespondant = table2.champCorrespondant
```

```sql
-- Je veux récupérer les articles dont l'auteur s'appelle Vincent

-- Le select fonctionne comme ce qu'on connait dejà, 
-- mais ici comme on a plusieurs tables (parce qu'une jointure) on spécifie éventuellement le nom de la table
-- En préfixe du champ, nécessaire si il y a le m^ême nom de champ dans les deux tables (exemple ici id)
SELECT title, name, author.id,  post.id
-- On va chercher les données sur deux tables différentes: post et author
-- En gros on récupère deux tables
FROM post JOIN author 
-- On doit spécifier à quel endroit se fait la liaison entre les deux tables
-- On dit que le champ de la table post "author_id" correspond au champ "id" de la table author
ON post.author_id = author.id
-- On spécifie la condition de ce qu'on veut récupérer,
-- Ici on récupère les articles dont l'auteur s'appelle Vincent
WHERE author.name = 'Vincent'
```

- Grosse jointure vénère:

```sql
SELECT champs
FROM table1 JOIN table2 
ON table1.champCorrespondant = table2.champCorrespondant
JOIN table3
ON table2.autreChampQuiLieLa2Etla3 = table3.autreChampQuiLieLa2Etla3
```