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
**$ git init** : Permet d'initaliser un répertoire local en répertoire GIT. Un dossier .git est créé à l'intérieur de ce répertoire permettant ainsi de gérer les versions du projet

**$ git status** : Liste tous les nouveaux fichiers et les fichiers modifiés à commiter

**$ git add** : Permet d'ajouter dans la Staging Area un ou plusieurs fichiers *(Ex : $ git add fichier.txt fichier.php)*

**$ git commit -m 'Message'**: Enregistre une version des fichiers disponibles dans la Staging Area et nomme avec un message les changements effectués *(Ex : $ git commit -m 'Ajout de la gestion des sotcks')*

**$ git push** : Dépose sur le repository distant les commits

**$ git pull** : Récupère la dernière version disponible sur le repository distant en la mettant sur notre repository local

**$ git clone** : Télécharge un projet et tout son histoire de versions *(Ex : $ git clone htttp://lien-du-projet)*

**$ git log**: Avoir le journal du projet 

**$ git diff** : Montre les différences de contenus entre notre version actuelle et la dernière version commitée

**$ git config --global user.email "votre-email@email"** : Définit l'email qui sera associé aux opérations de commit

**$ git config --global user.name "votre_nom"** : Définit le nom qui sera associé aux opérations de commit

**$ git stash** : Enregistre de manière temporaire des fichiers modifiés qui ne seront pas ajouter à la staging area

**$ git checkout** : Permet de remettre un fichier dans l'état du dernier commit

**$ git show *n°chat*** : Affiche le commit demandé (utiliser ctr+q pour sortir)  




La gestion de conflit 
---------------------

**$ git pull** : Récupérer la dernière version du repository distant

**$ git status** : Indique les fichiers que GIT ne parvient pas à merger

**$ git diff** : Indique le contenu du conflit, la partie *HEAD* étant notre version et *========* la version du repository distant

**Ouvrir le fichier avec l'éditeur de texte** : Choisir les parties à conserver et supprimer l'ensemble des marques de merge *HEAD* et *====*

**$ git add *lefichier*** : Ajouter dans la staging area le fichier modifié

**$ git commit** : Il n'est pas nécessaire d'ajouter un message car GIT sait qu'il s'agit d'une résolution de conflit

**$ git push** : Ajouter sur le repository distant le fichier

*S'il y a une nouvelle erreur, recommencer le processus*




