# PostgreSQL

Documentation PostgreSQL :
- https://www.postgresql.org/docs/
- https://node-postgres.com


## DANS LE TERMINAL

### installer PostgreSQL dans le projet

`npm i pg` ou `npm install pg`

#### sur mac 

passer par brew : c'est un gestionnaire de package, s'il est installé sur ton mac, il suffit de faire `brew install postgresql` : https://gist.github.com/ibraheem4/ce5ccd3e4d7a65589ce84f2a3b7c23a3

### Vérifier la version

`psql —version`

### Se connecter en super Admin

`sudo -i -u postgres`

Ce qui nous fait arriver sur : `postgres#`

### Afficher tous les utilisateurs de bdd existants
`\l`

### Créer un Utilisateur de BDD

`CREATE ROLE nom_user WITH LOGIN PASSWORD ‘mdp’;`

ou crypté : 

`CREATE ROLE nom_user WITH LOGIN ENCRYPTED PASSWORD ‘mdp’;`


### Se connecter à un utilisateur qu'on a créé

`psql -U nom_user`

Ca demande le mot de passe : se mot de passe restera transparent. Taper sur entrer pour valider.


### Modifier le mot de passe d'un utilisateur

`ALTER ROLE trombi PASSWORD ‘lenouveaupsw'`


### Créer une BDD

`CREATE DATABASE nom_bdd OWNER ‘nom_user’;`


### Se connecter à une BDD qu'on a créé

`psql -U nom_user -d nom_bdd -f fichier.sql `


## DANS VSC

### Paramétrer la BDD dans le .env

- version longue

```
PORT=3000
PGUSER=game
PGHOST=localhost
PGPASSWORD="game"
PGDATABASE=game
PGPORT=5432
```

- version courte avec PG_URL
  
`PG_URL=psql://PGUSER:PGPASSWORD@PGHOST:PGPORT`

Ex :
`PG_URL=psql://trombi:trombi@localhost:5432/trombi`

Ex sur serveur distant : 
`PG_URL=psql://PGUSER:PGPASSWORD@PGHOST:PGPORT`
`PG_URL=psql://trombi:trombi@database.server.com:5432/trombi`


### Connecter la BDD avec un fichier.sql

Depuis etudiant@teleporteur dans le terminal (et dans le dossier data/ si on ne veut pas devoir écrire le chemin pour y accéder): 

`psql -U nom_bdd -f chemin/database.sql` 


### Déconnecter la BDD

- sortir de postgres=# : \q
- sortir de notre bdd : ctrl D

## Connexion avec Express

1. On créé un client (qui va se connecter a un serveur)
2. on lui spécifie `host`, `user`, `password` et `database` (on lui spécifie a quel endroit se connecter, quel utilisateur utiliser, quel base de donnée et le mot dd passe)
 
```
Const client = new Client({
    Host: …,
    User: …,
    Password: …,
    Database: ‘prof’,
});
```

3. on lui dit de se connecter
`client.connect();`

4. on fait nos requêtes

On utilise la méthode query sur le client dans une méthode de dataMapper
On lui passe en paramètre un callback (et éventuellement une info nécessaire à la requête comme un id par exemple) : 

Exemple pour une liste d'objets à récupérer : 
   ```
   getAllFigurines: (callback) => {
        client.query(`
            SELECT 
                figurine.*, 
                round(avg(review.note)) AS avg_note 
            FROM figurine
            JOIN review ON figurine.id = review.figurine_id
            GROUP BY figurine.id
            ORDER BY name
        `, callback);
    },
    ```

Exemple pour un seul objet à récupérer : 
 ```
    getOneFigurine: (id, callback) => {
        const preparedQuery = {
            text: `
                SELECT
                    figurine.id AS id,
                    figurine.name AS name,
                    figurine.description AS description,
                    figurine.size AS size,
                    figurine.price AS price,
                    figurine.category AS category,
                    review.author AS author,
                    review.note AS note,
                    review.title AS title,
                    review.message as message,
                    avg(review.note) OVER() as avg_note
                FROM figurine 
                JOIN review ON review.figurine_id = figurine.id
                WHERE figurine.id = $1
            `,
            values: [
                id
            ]
        }
        client.query(preparedQuery, callback);
    }
```
