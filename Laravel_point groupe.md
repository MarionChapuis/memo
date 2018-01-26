# Laravel Point groupe 


Trio gagnant : route -> Controller -> Vue

* Route : /boissons (href="boissons")
* Controller : BoissonController
* Vue : boisson.list



## Helpers

| Helper | Définition | Exemple
| :-----:| :---------:| :-------:|
| url() | retourne le chemin absolu d'une URL | {{ url('/boisson') }}
| route() | retourne la route avec des paramètres si nécessaire | {{ route('boissons.list', $id) }}
| Route::get(..)->name(nomRoute) | Donne un nom à une route | ->name(boissons.list)


## Route avec paramètres

* Route : boissons/{id} 
* Fonction : show($id)


## Description fonctionnelle

| Action | Méthode du controller | Route
| :-----:| :---------:| :-------:|
| Liste | list | /x/
| Detail | show | /x/{id}
| Afficher Formulaire Création | create | /x/create
| Traiter Formulaire création | store | /x/    (Post)
| Afficher Formulaire Edition | edit | /x/{id}/edit
| Traiter Formulaire Edition | publish | /x/{id}   PUT
| Supprimer | delete / /x/{id}    DELETE


Post : créer 
Put : modifier 


## Migration 

Description de comment est notre BDD.
Instance d'un objet qui représente une table avec plein de méthodes.
Permet aux autres de récupèrer la structure : php artisan migrate


## ORM : eloquent

Se charge de la BDD (ajout, suppression, modification...) peu importe le SGBD (Mysql...)
* Commande pour créer le modèle : php artisan make:model Nomsingulier (ex: Boisson) -m






Nommage :

nom table : pluriel minuscule
nom model : une Majuscule singulier 
nom Controller : une Majuscule singulier

return view(boisson.list)
boisson.list = boisson/list

