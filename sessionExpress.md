# LES SESSIONS AVEC EXPRESS-SESSION

Documentation : https://npmjs.com/package/express-session

## Pourquoi créer une session ?

Les cookies apparaissent en clair dans les headers côté client. C'est donc difficile de maintenir des informations sensibles en les utilisant? Cependant on s'en servira tout de même afin de récupérer les données de l'utilisateur dans un ID stocké dans un cookie.

## Module express-session

### Installation

- #### Dans le terminal :

  ```bash
  npm install express-session
  ```

- dans le server dans `index.js` :
  ```js
  const session = require('express-session');
  ```

## Lancer une session

Pour lancer une session, voici le code suivant (extrait de la documentation) dans `index.js` :

```js
var app = express()
app.set(trust proxy, 1);
app.use(session({
    secret: 'keyboard cat',
    resave: false,
    saveUninitialized: true,
    cookie: {secure: true}
}));
```

- **Secret** : clé de cryptage pour les informations de l'utilisateur (sorte de mdp)
- **Resave** : L'option **resave** permet de réinitialiser la durée de vie de la session même si aucune valeur n'a été mise à jour. une requête suffit (true : relance la durée de vie à chaque connexion)
- **saveUninitialized** : true -> sauvegarde dès le début sans qu’on ait rien mis. On créé la session même si l'on ne stocke aucune information dedans.
- **Cookie** : objet (une propriété qui dit sécurité oui ou non)

### Où trouver le cookie

Dans le navigateur, relancer la page, puis dans la console, onglet Application on peut voir le cookie **connect.sid** avec en valeur une clé qui contient une string.
