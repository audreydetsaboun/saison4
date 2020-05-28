# SQL

## CREATE


## READ

### SELECT FROM

```
SELECT * FROM <table>;
SELECT <colonne1>, <colonne2> FROM <table>;
```

### WHERE

WHERE permet de filtrer les résultats de la requête : 

```
SELECT <colonne> FROM <table> WHERE <colonneN> = x;
SELECT * FROM student WHERE id = 5;
```



## UPDATE


## DELETE


## FONCTIONS

### count()

La fonction `count()` permet de compter le nombre d’enregistrements au lieux de sortir chacune d’elles. 

Elle peut être limitée par un filtre WHERE : 
`SELECT count(*) AS nombre_prof_JS FROM prof WHERE Spe_js = true;`

### max() et min()

```
SELECT max(age) AS age_maximum FROM prof;
SELECT min(age) AS age_minimum FROM prof;
```

### AS

AS permet de nommer différemment les données issus de l’opération (ici les colonnes
SELECT first_name AS prénom FROM prof;)

`SELECT <colonne> AS nouveau_nom FROM <table>;`