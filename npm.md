# NMP

Documentation : https://www.npmjs.com/get-npm

## Vérifier que Node et NPM sont installés

(installer node, installe automatiquement npm)

`node -v `

`npm -v`


## update NPM

`npm install npm@latest -g`


## initier un projet

Cela créera le `package.json`sur lequel seront rattachées les dépendances que l'on installera.

`npm init`


## installer des dépendances 

`npm install express ejs` ou `npm i express ejs`


## lancer le serveur

- `node index.js` 
- `nodemon index.js` permet de maj dès qu'on modifie les fichiers sans avoir à fermer et relancer le serveur

## npm run dev / npm start

Aller dans package.json et ajouter les lignes suivantes dans "scripts" : 

```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    __"dev": "nodemon index.js",__
    __"start": "node index.js"__
},
```

- équivalent node : `npm start`
- équivalent nodemon : `npm run dev`


## relancer le serveur sans quitter nodemon ou npm run dev

`rs`


## fermer le serveur

raccourcis clavier : ctrl + C

## tuer le port d'écoute

sur le port 3000 : `kill -9 $(lsof -t -i:3000)`
sur le port 1234 : `kill -9 $(lsof -t -i:1234)`

