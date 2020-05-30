# GESTION DE PROJET AGILE SCRUM

## Méthode agile

![schéma agile](https://www.ludotic.com/wp-content/uploads/m-agile_titre.jpg)

A la différence du **cycle en V**, la **méthode agile** permet de présenter le produit au client en cours de développement. Les tâches sont regroupées par itérations afin d'avoir un produit à présenter avec un minimum de fonctionnalités pour avoir un retour client et savoir s'il on est sur la bonne voie. Cela permet de rectifier le tir en cas de besoin avant d'avoir travailler sur le projet entier.

## Collecter les informations du client

## Analyser la demande

Reformuler en phrases simples sans penser technique. Préciser :

- Ce que l’application doit faire
- Ce qu’elle ne fait pas

## Use cases & Sprints

- ### Use Cases

  Extraire l'expression du besoin. Pour cela, réaliser un tableau de Use Cases.

- ### Sprints
  **Découpage en sprint** : Un sprint = une itération => . Il faut qu’à l’issu de chaque sprint, on puisse montrer l'application au client. les sprints permettent aussi d'avoir un retour du client et donc un ajustage si nécessaire (= cela évite de s'écarter du chemin et d'être hors sujet par rapport à la demande du client). La durée de chaque sprint doit être équivalente.

_Exemple :_

| en tant que | j’ai besoin de…                    | afin de…                      | sprint |
| ----------- | ---------------------------------- | ----------------------------- | ------ |
| Visiteur    | accéder à la page d'accueil        | présententation               | 1      |
| Visiteur    | accéder à la liste des thématiques | afin de pré filtrer les quizz | 1      |
| Visiteur    | Créer un compte                    | Pour participer au quizz      | 2      |
| Visiteur    | Me connecter                       | Pour répondre                 | 2      |
| Membre      | Se deconnecter                     | -                             | 2      |

## Préparer les Wireframes :

Itinéraire d'une maquette :

![itinéraire_maquette](/images/itinéraire_maquette.png)

Dans la partie conception ergonomique, plus précisément le Wireframe :

![schema_wireframe](/images/wireframe.png)

### Mobile First

Aujourd'hui, la part des internautes mobile est plus forte que celle des internautes desktop. Il est donc important de réaliser les wireframes d'abord en version mobile puis en version desktop.

![mobile_wireframe](/images/mobile_wireframes.png)

Quelques sites gratuits pour réaliser les wireframes :

- http://wireframe.cc
- https://whimsical.com/
- https://www.figma.com/wireframe-tool/
- https://marvelapp.com/features/wireframing
- https://www.adobe.com/products/xd.html

## Kanban

Tableau de suivi qui permet de répertorier et classer :

- ce qu’on a à faire : **backlog**,
- ce qu’on est entrain de faire : **in progress**
- ce qu’il reste à faire : **done**

Etapes :

1. Création du Kanban dans l’onglet Projects du repo github

2. Créer 3 colonnes : backlog, in progress, done

3. Créer les tâches des Use Cases dans la colonne Backlog du Kanban

## Méthode Merise

Conception de la base de données grâce à 2 schémas :

- **MCD** : Modèle Conceptuel de Données
- **MLD** : Modèle Logique de Données

### MCD

Le MCD permet de réfléchir à ce que vont être :

- les entités : les tables,

- les utilisateurs : les types d'utilisateurs qui accèderont à l'application web,

- les liaisons : lien entre 2 entités,

- les verbes de liaison : qualifie la liaison entre 2 entités. Si on ne trouve pas de mot qualifiant la liaison, on met DF : Dépendances Fonctionnelle,

- les cardinalités : valeur minimal et maximale des associations

Outils de conception gratuit en ligne : http://mocodo.wingi.net/

#### Fiche récap du MCD :

https://github.com/O-clock-Alumni/fiches-recap/blob/master/bdd/conception-03-mcd.md

### MLD

Le MLD permet de voir se dessiner la future base de données. On y retrouve le nom des tables, avec leurs colonnes et leur typage. C'est une étape intermédiaire entre le MCP et le MPD (Modèle Physique de Données).

#### Fiche récap du MLD : https://github.com/O-clock-Alumni/fiches-recap/blob/master/bdd/conception-04-mld.md

#### FIche récap du MPD : https://github.com/O-clock-Alumni/fiches-recap/blob/master/bdd/conception-05-mpd.md
