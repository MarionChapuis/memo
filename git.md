Mémo GIT - Marion Chapuis
=========================


Git et GitHub
-------------

**GitHub** est une plateforme permettant de stocker des projets Git.

**Git** permet de gérer les versions d'un projet et donc de collaborer à plusieurs sur un même projet.



Schéma explicatif
-----------------

**Staging area** : Permet de choisir finement le contenu du prochain commit, c'est une zone tampon


![Schéma Git](https://raw.githubusercontent.com/MarionChapuis/memo/master/Schema_git.png)



Les commandes GIT 
-----------------
**$ git init** : Permet d'initialiser un répertoire local en répertoire GIT. Un dossier .git est créé à l'intérieur de ce répertoire permettant ainsi de gérer les versions du projet

**$ git status** : Liste tous les nouveaux fichiers et les fichiers modifiés à commiter

**$ git add** : Permet d'ajouter dans la Staging Area un ou plusieurs fichiers *(Ex : $ git add fichier.txt fichier.php)*

**$ git commit -m 'Message'**: Enregistre une version des fichiers disponibles dans la Staging Area et nomme avec un message les changements effectués *(Ex : $ git commit -m 'Ajout de la gestion des sotcks')*

**$ git push** : Dépose sur le repository distant les commits

**$ git pull** : Récupère la dernière version disponible sur le repository distant en la mettant sur notre repository local

**$ git clone** : Télécharge un projet et tout son histoire de versions *(Ex : $ git clone http://lien-du-projet)*

**$ git log**: Avoir le journal du projet 

**$ git diff** : Montre les différences de contenus entre notre version actuelle et la dernière version commitée

**$ git config --global user.email "votre-email@email"** : Définit l'email qui sera associé aux opérations de commit

**$ git config --global user.name "votre_nom"** : Définit le nom qui sera associé aux opérations de commit

**$ git stash** : Enregistre de manière temporaire des fichiers modifiés qui ne seront pas ajoutés à la staging area

**$ git checkout** : Permet de remettre un fichier dans l'état du dernier commit

**$ git show *n°chat*** : Affiche le commit demandé (utiliser ctrl+q pour sortir)  




La gestion de conflit 
---------------------

**$ git pull** : Récupérer la dernière version du repository distant

**$ git status** : Indique les fichiers que GIT ne parvient pas à merger

**$ git diff** : Indique le contenu du conflit, la partie *HEAD* étant notre version et *========* la version du repository distant

**Ouvrir le fichier avec l'éditeur de texte** : Choisir les parties à conserver et supprimer l'ensemble des marqueurs de merge *HEAD* et *====*

**$ git add *lefichier.txt*** : Ajouter dans la staging area le fichier modifié

**$ git commit** : Il n'est pas nécessaire d'ajouter un message car GIT sait qu'il s'agit d'une résolution de conflit

**$ git push** : Ajouter sur le repository distant le fichier

*S'il y a une nouvelle erreur, recommencer le processus*




## Pull Request

Un pull request permet de demander d'écrire sur un projet. Le principe est de faire une branche pour travailler dans son coin puis effectuer une pull request. 
Si le propriétaire du projet est d'accord, il mergera la branche avec master. 

#### Etapes pour créer une Pull Request :

* Fork du projet
* Cloner le projet en local
* Effectuer un git pull origin master (pour garantir qu'on est à jour si on ne vient pas de cloner le projet)
* Créer une branche 
```bash
git checkout -b Nom-ma-branche
```
* Effectuer son travail 
* Add, commit et push sur la branche
* Si le repo sur Github ne connait pas la branche, il faut donc l'ajouter lors du push:
```
git push --set-upstream origin nomMaBranche
```
* Sur Github, cliquer sur "new pull request" (ou sur le message en jaune proposant de faire le pull request)
* Choisir comme "base" notre projet sur master et dans "compare" choisir notre branche
* Utiliser Writer (et preview) pour laisser des messages explicites (listes à puces, copies d'écran...)
* Cliquer sur "Create Pull Request"

#### Etapes pour valider et merger :

Pour le propriétaire du projet, il peut valider la pull request en mergeant avec Master.

* Sur Github aller dans l'onglet "Pull Requests"
* Sélectionner la pull request
* Cliquer sur "Merge pull request" pour valider et merge

Il est possible de voir les commits sur la pull request, les fichiers changés mais aussi laisser des commentaires et ne pas valider la pull request.

Tant que la pull request reste ouverte, le développeur peut continuer son travail et pusher sur la branche pour la mettre à jour.


## Créer un backlog avec Github

Etapes:
* Se positionner dans notre projet
* Onglet "Projects"
* Choisir "New Project"
* Donner un nom, renseigner la description et choisir comme template "Basic Kanban"
* Cliquer sur "Create project"
* S'afficher alors la structure "To do, In Progress, Done"

Il est possible d'ajouter des colonnes et créer un backlog par branche...
