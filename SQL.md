# SQL

## CREATE

- ### CREATE TABLE :

```sql
CREATE TABLE IF NOT EXISTS "nom_table1" (
    "id_table1" SERIAL PRIMARY KEY,
    "nom_colonne2" VARCHAR(128) NOT NULL,
    "nom_colonne3" VARCHAR(255) NOT NULL,
    "nom_colonne4" INT (128) NOT NULL,
    "nom_colonne5" VARCHAR(64) NULL
    "nom_table2_id" INT,
    FOREIGN KEY("nom_table2_id") REFERENCES "nom_table2"("id_table2")
);
```

*Pour les id, on peut rajouter **PRIMARY KEY** qui signifie clé primaire, non nulle et unique dans la colonne (et créé un index).*

*__FOREIGN KEY__ veut dire clé étrangère et permet de relier 2 tables entre elles.*

- ### INSERT INTO

**SERIAL** : créé une fonction automatique qui nous renverra toujours une valeur différente à chaque appel. Pour l’appeler lors des **INSERT INTO** on utilisera le mot clé **DEFAULT** dans la colonne appropriée.

```sql
INSERT INTO "table"("id", "name", "element", "level", "value", "visual_name" ) VALUES 
(DEFAULT, 'Bogomile', null, true, 1, 'Bogomile.jpg' ), 
(DEFAULT, 'Fungus', null, false, 5, 'Fungus.jpg' ), 
(DEFAULT, 'Elmidea', null, true, 1, 'Elmidea.jpg' );
```

## READ

- ### SELECT FROM

```sql
SELECT * FROM <table>;
SELECT <colonne1>, <colonne2> FROM <table>;
```

- ### WHERE

WHERE permet de filtrer les résultats de la requête : 

```sql
SELECT <colonne> FROM <table> WHERE <colonneN> = x;
SELECT * FROM student WHERE id = 5;
```

- ### ORDER BY

```sql
SELECT * FROM <nom_table> ORDER BY <colonne> ASC;
SELECT * FROM <nom_table> ORDER BY <colonne> DESC;
```

- ### GROUP BY

La commande `GROUP BY` permet de regrouper des enregistrements ayant des valeurs en commun. Objectif : réaliser des stats sur un paramètre particulier.
En général on l'utilise avec une fonction SQL permettant de compter, de faire une moyenne, de récupérer le minimum ou le maximum.

```SQL
SELECT <colonne_stat>, count(*) AS total FROM <table> GROUP BY <colonne_stat>;
```

### LIMIT

Grâce au mot clé `LIMIT` on peut limiter le nombre d'enregistrement en sortie de résultat. Cela est très utile lorsque l'on veut paginer des résultats alliés au mot clé `ORDER BY`
Pour les page suivantes, on rajoutera le mot clé `OFFSET` qui défini à partir de quel occurrence d'enregistrement on débute la sortie.

```SQL
SELECT * FROM <nom_table>
ORDER BY <colonne1>
OFFSET 100 LIMIT 10;
```

- ### AS

AS permet de nommer différemment les données issus de l’opération.

```sql
SELECT <colonne> AS nouveau_nom FROM <table>;
```

Exemple : 
```sql
SELECT first_name AS prénom FROM prof;
```

- ### JOINTURES

```sql
SELECT *
  FROM table1 
  JOIN table2 
    ON table2.foreign_key = table1.primary_key
 WHERE table1.primary_key = $1
;
```

## UPDATE

- ### UPDATE ... SET

Update sert à mettre à jour les informations des champs d'une table.

*ATTENTION : ne pas oublier le `WHERE` sur les `UPDATE` sinon on modifie toutes les lignes.*

```sql
UPDATE <nom_table> SET <colonne1>=<value1>, <colonne2>=<value2> 
WHERE <colonne3>=<value3>;
```

- ### ALTER TABLE
Alter table  sert à modifier la structure d'une table.

Afin de modifier la structure d'un table on peut utiliser la commande `ALTER TABLE` qui est une commande d'encapsulage pour définir différentes actions, comme ajouter (`ADD`), supprimer (`DROP`), modifier (`ALTER`), renommer (`RENAME`) une colonne, ou toute autre opération directement liée à sa structure.

```SQL
ALTER TABLE <nom_table>
    ADD COLUMN <nom_nouvelle_colonne> <type_nouvelle_colonne> <options_nouvelle_colonne>
    ALTER COLUMN <colonne1> <type_colonne1> <option_colonne1>
    RENAME COLUMN <colonne2> TO <nouveau_nom_colonne2>
    DROP COLUMN <colonne3>;
```




## DELETE

_**attention existe mais COMMANDES DANGEREUSES !!!**_

- ### DELETE
  
```sql
DELETE FROM prof WHERE id=4; -- ne jamais DELETE sans un WHERE
```

- ### TRUNCATE TABLE

Supprime tous les enregistrement d'un table. Equivalent à `DELETE FROM <nom_table>`.

```sql
TRUNCATE TABLE <nom_table>; -- ne jamais faire en prod
```

- ### DROP TABLE

Supprime la table et toutes les données qui sont dedans.

```SQL
DROP TABLE <nom_table>;
```

<hr>


## QUELQUES FONCTIONS SQL

- ### count()

La fonction `count()` permet de compter le nombre d’enregistrements au lieux de sortir chacune d’elles. 

Elle peut être limitée par un filtre `WHERE` : 
```sql
SELECT count(*) AS nombre_prof_JS FROM prof WHERE Spe_js = true;
```

- ### max() et min()

Les fonctions min et max permettent de récupérer le minimum et le maximum d'une colonne dans une table en fonction du filtre.

```sql
SELECT max(age) AS age_maximum FROM prof;
SELECT min(age) AS age_minimum FROM prof;
```

- ### upper et lower

Les fonctions upper et lower permettent de modifier la casse d'un colonne ou d'une chaîne de caractère.

```SQL
SELECT * FROM <nom_table> WHERE upper(<colonne1>) = upper('<chaine_de_caractère>');
```

## Pro tips

Comment récupérer le nombre total d'enregistrement filter alors que l'on effectue une pagination avec un `LIMIT` ?

- ### over()

Avec la requête suivante on récupère à la fois les 10 enregistrement et l'information du comptage sans la limitation dans une colonne "total"

On pourrait traduire le terme "over" par le fait qu'il ne respecte pas la restriction de groupage, lors de l'utilisation de la function `count()`.

Dixit Florian Lefeuvre : "Ca lui passe au dessus quoi".

```SQL
SELECT *, count(*) OVER() AS total FROM <table> WHERE <condition> LIMIT 10;
```