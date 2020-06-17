VERSIONNER LES FICHIERS

Repository (représentation de l’état du projet)

Remote repository : accessible par tout le monde (exemple: GitHub)
Local repository : petit serveur git en local sur l'ordi
Disque dur : le disque dur

Git clone : recupérer un remote repository

Récupéré les modifications du remote vers local : pull
Renvoyer vers local : commit
Enregistrer du local vers le remote : push

Git status
Add = dire quels fichiers ou bout de fichier que je vais envoyer dans mon prochain commit (préparer un colis Amazon)
Git add myDirectory ou git add fichier.js
Git add -p = par partie
Git commit -m "message"= enregistrer ce que j’ai add du dd vers le local repository
Git push = pousser les commit sur le remote repository
Git log = voir tous les commit

Créer un nouveau repository dans GitHub, copier l’url créée puis :

…or create a new repository on the command line

echo "# git2" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/audreydetsaboun/git2.git
git push -u origin master

…or push an existing repository from the command line

git remote add origin https://github.com/audreydetsaboun/git2.git
git push -u origin master
Git remote -v (connaitre le dossier remote repo)
Git pull pour mettre a jour avec les modifications qui ont été faites sur git hub

Les branches
[git Flow][gitflow.jpg]
Pour créer une branche : git checkout -b nomdebranche
Pour changer de branche : Git checkout nomdebranche
Pour pusher une nouvelle branche vers le remote : git push -u origin nomdebranche
Connaitre liste des branches locales : git branch
Connaitre liste des branches remote : git branch --remote
Fusionner les branches (merger) : se mettre sur la branche où l’on veut recevoir les commit (développe) : git merge feature (pour ramener les commit de feature sur develop)

REBASE
Ne jamais faire de rebase sur master
Ne jamais faire une rebase sur une branche partager
Git rebase (être sur la branche ou on veut récupérer les commit)
Git rebase - - continue (continuer après avoir gérer un conflit)
Git rebase - - abort (arrêter)

Git rebase interactif : modifier les commit => git rebase -i nomdelabranchedistante
Donne ces possibilités :

- p, pick = use commit
- r, reword = use commit, but edit the commit message
- e, edit = use commit, but stop for amending
- s, squash = use commit, but meld (melanger) into previous commit
- f, fixup = like "squash", but discard this commit's log message
- x, exec = run command (the rest of the line) using shell
- d, drop = remove commit
  Git rebase -i nom de branche : depuis la branche feature on appelle la branche développé, permet de rejouer les commits des 2 branches, voir où sont les conflits et les régler, avant de pouvoir merger.

Git commit - -amend (après un git add sur ce qu’on a modifié, ramène le dernier commit pour le modifier)

quand on fait des tout petits changements après un commit, qui ne nécessitent pas un nouveau commit, et avant d'avoir pushé :
git commit --amend --no-edit

Ctrl + o pour sauvegarder, entrer pour valider, ctrl + x pour sortir

Voir le détail du commit : git show n°duCommit

git remote -v
git remote remove origin
git remote add origin nouvelle adresse de clone
: changer de repo pour l’enregistrement des motifs

Git stash : sauver des fichiers dans une petite boite
Git stash pop : rapatrier le dernier stash dans une nouvelle branche ou qu’on a pull les MAJ des autres (pour reprendre notre travail ou il en était sans le perdre
Git stash list
Git stash show idStach
Git stash pop idStash

Git reset n°commitAuquel on veut revenir : effacer les commit après le n°de commit indiqué
Git reset - - soft n°commit : tous les commit en staged (en add)
Git reset - - mixed n°commit : meme pas en add
Git reset - - hard n°commit : efface tout les commit après
Git reset HEAD^nbre de commit en arrière depuis le head (head comptant pour 1)
Annuler : git reset HEAD (tant que ça a pas été push, y’a la sauvegarde en remote, donc on récupère grâce au remote)
Git push -f : pour forcer le push malgré l’effacement des commit
Cherry-pick : prendre un commit d’une autre branche et le ramener sur la branche où l’on se situe

Dangereux :
Pour effacer le code non commité depuis le dernier pull :
git reset --hard HEAD
