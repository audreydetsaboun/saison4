# Application Express avec architecture MVC

### Prérequis NPM : 
installer les packages express, ejs, dotenv, pg

### ROUTER

1. créer un fichier router.js
2. require express
3. require les modules controller
4. créer un router avec express.Router()
5. créer nos routes avec router.get
6. passer en 1er paramètre le chemin url entre côte (ex: '/' ou '/article/:id')
7. passer en 2e (et Nième) paramètre les méthodes du controller que l'on veut appliquer (ex: mainController.homePage, cartController.deleteFromCart)
8. exporter le module router


### SERVER

1. créer un fichier index.js
2. require express
3. require dotenv et appeler sa méthode .config()
4. créer un fichier .env et un fichier .env.example (paramétrer les infos dans le .env)
5. paramétrer le port d'écoute (`const PORT = process.env.PORT || 1234;`)
6. require le router
7. require le dataMapper si besoin
8. lancer express (`const app = express();`)
9. mettre en place le moteur de rendu (`app.set('view engine', 'ejs');`)
10. configurer le chemin vers les vues ejs (`app.set('views', 'app/views');`)
11. configurer le chemin vers les fichiers statiques (`app.use(express.static('public'));`)
12. dire d'utiliser le router (`app.use(router);`)
13. dire à l'appli d'écouter
14. passer en 1er paramètre le port d'écoute
15. optionnel, passer en 2e paramètre un `console.log('Listening on ${PORT}');` (attention ce sont des ` dans les parenthèses)




# MVC avec Express

## MODELE

**Le modèle représente les datas, autrement dit la base de données.**

- ### Créer un module qui relie et connecte la BDD à l'appli
1. créer un fichier js (database.js par exemple)
2. require le package pg (PostgreSQL)
3. créer un 'client'
4. connecter le client
5. exporter le module


- ### créer un module dataMapper
1. créer un fichier js (dataMapper.js par exemple)
2. require le module créé précédemment (database.js) et le stocker dans une constante (const client par exemple)
3. créer un module dataMatter
4. y placer les méthodes dont on a besoin (getOneStudent, getAllPromo par exemple), avec un callback en paramètre ainsi que toute information nécessaire pour la méthode query qui suit
5. appliquer la méthode .query sur notre bdd (client.query par exemple)
6. passer notre requête en 1er paramètre (ex: SELECT * FROM prof;)
7. passer les paramètres de notre dataMapper.méthode en second paramètre de notre méthode query
8. exporter le module


## VUE

**La vue représente l'interface envoyée à l'utilisateur, autrement dit les pages EJS.**

C'est du code HTML. Lorsqu'il y a besoin d'inclure des données, on ouvre les balises suivantes : 
- `<% %>` pour du code javascript (exemple des boucles ou des if)
- `<%= %>` pour afficher des variables
- `<%- %>` pour inclure des partials
- `<%# %>` pour inclure des commentaires qui ne seront pas visibles dans la console du navigateur


## CONTROLEUR

**Le contrôleur permet d'avoir un intermédiaire entre la vue et le modèle.**

1. require le module dataMapper
2. créer notre module controller
3. créer les méthodes qui permettrons de traiter et envoyer les données à la vue (ex : homePage, figurineDetails, searchPage)
4. leur passer en paramètre request, response et au besoin next
5. créer une constante pour stocker les informations récupérées par l'url (request.params.id) et le convertir en Int (parseInt / Number)
6. capturer si ce n'est pas un nombre (next() et return)
7. appeler la méthode du dataMapper dont on a besoin
8. passer en paramètre la constante créée précédemment si la méthode en a besoin
9. passer en paramètre le callback(error,result)
10. capturer l'erreur s'il y en a une et return
11. faire un response.render pour renvoyer une page
12. passer en premier paramètre la vue à renvoyer
13. passer en 2e paramètre les informations sous forme d'un objet
14. exporter le module
