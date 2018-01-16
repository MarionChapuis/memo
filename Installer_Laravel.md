# LARAVEL 5.5

Tuto utilisé : [Lien tuto Installation Laravel 5.5](https://laravel.com/docs/5.5/installation)

**Vérifier que la version de notre PHP est supérieure à 7.**

Touches : windows + pause 
Choisir : 
* paramètres systèmes avancés
* variables d'environnement
* double clic sur PATH

* *S'il n'y a pas la bonne version PHP dans le chemin d'accès* :
	* Nouveau
	* Copier le chemin : C:\wamp64\bin\php\php7.0.23
	* OK

Réouvrir Bash, vérifier la version de PHP en entrant la commande : 
$ php -v 

Télécharger Composer via le lien : [Lien téléchargement](https://getcomposer.org/download/)
*Lors de l'installation vérifier le chemin d'accès : wamp64\bin\php\php.exe*

Réouvrir Bash et entrer la commande : 
composer 
*les informations sur composer doivent s'afficher*


Entrer la commande : composer global require "laravel/installer"
Installation des composants

Ouvrir Bash dans le répertoire où l'on souhaite mettre notre projet 
commande : laravel new NomProjet 
Installation des composants

Ouvrir Bash à l'intérieur du dossier de notre projet
Commande : php artisan serve 

Les lignes suivantes apparaissent : 

> Laravel development server started: <http://127.0.0.1:8000>
[Mon Jan 15 10:53:15 2018] 127.0.0.1:52136 [200]: /favicon.ico
[Mon Jan 15 10:54:07 2018] 127.0.0.1:52137 Invalid request (Unexpected EOF)
[Mon Jan 15 10:54:07 2018] 127.0.0.1:52139 Invalid request (Unexpected EOF)

Vérifier la version de Laravel :
Commande : $ php artisan --version

La ligne ci-dessous apparait en indiquant la version de Laravel
Laravel Framework 5.5.28

Pour ouvrir la page d'accueil de Laravel :
Ouvrir dans le navigateur : localhost:8000


Entrer commande :
$ php artisan serve 

**Ne pas sortir de cette commande pour pouvoir afficher la page d'accueuil Laravel**



## Modifier la page d'accueil de Laravel 

* Avec Sublime, choisir **file/open folder**
* Choisir le dossier du projet 
* S'ouvre alors dans l'éditeur de texte Laravel avec tous les dossiers
* Sélectionner : *resources/views/welcome.blade.php*
* Modifier le fichier PHP pour afficher le message que l'on souhaite

## Créer d'autres pages 

* Dans resources/views : créer un nouveau fichier avec le nom "monfichier.blade.php"
* Créer la page
* Dans Sublime Text, pour ouvrir : ctrl + p
* Taper : rweb et cliquer dessus (le fichier s'ouvre)
* Ajouter le chemin : 
```php
Route::get('nomdufichier', function () {
    return view('nomdufichier');
});
```
* Ouvrir le navigateur : localhost:8000/nomdufichier


## Qu'est-ce que Composer ?

**Composer est un outil pour gérer les dépendances en PHP.** 
Les **dépendances**, dans un projet, ce sont toutes **les bibliothèques** dont votre projet dépend pour fonctionner.
Par exemple, votre projet utilise la bibliothèque SwiftMailer pour envoyer des e-mails, il « dépend » donc de SwiftMailer. Autrement dit, SwiftMailer est une dépendance dans votre projet.

### Concrètement, comment ça marche ?
Concrètement, voici comment s'utilise Composer :

* On définit dans un fichier la liste des bibliothèques dont le projet dépend, ainsi que leur version ;

* On exécute une commande pour installer ou mettre à jour ces bibliothèques (et leurs propres dépendances donc) ;

 On inclut alors le fichier d'*autoload* généré par Composer dans notre projet.



*Exemple : michelf/markdown*

* Commande "composer init"
* Définir les différentes dépendances ? yes
* Commande "composer install"
* Importer dans la page le fichier "autoload.php" : 
```php
<?php 
	require "vendor/autoload.php"; 
?>
```

* Indiquer la librairie que l'on souhaite utiliser 
```php
<?php 
	require "vendor/autoload.php"; 
	use \Michelf\Markdown ; 
?>
```


## Installer la DEBUG BAR Laravel

* Ouvrir Git Bash dans le dossier du projet 
* Commande : *composer require barryvdh/laravel-debugbar --dev*
* Se rendre sur la page d'accueil Laravel pour vérifier la présence de la Debug Bar 


## Installer le Plugin Laravel dans Sublim Text

* "ctrl + shift + p" 
* Ecrire : Install
* Sélectionner : "Package Control : Install Package"
* "ctrl + shift + p" 
* Ecrire : Install
* Sélectionner : "Package Control : Install Package"
* Ouverture d'une nouvelle liste déroulante, choisir "Laravel 5 artisan"



## Installer l'IDE Helper sur PhpStorm

* Ouvrir Git Bash dans le dossier du projet
* Commande : *composer require barryvdh/laravel-ide-helper*
* Mettre à jour Composer, commande : *composer update*
* Ajouter dans le fichier config/app.php , à la fin du tableau "provider" : Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,
* Installer le package, commande : *composer require --dev barryvdh/laravel-ide-helper* (le --dev est à utiliser quand on est en local)
* Ajouter dans le fichier app/Providers/AppServiceProvider.php , dans la fonction register ()
```php
	public function register()
	{
	    if ($this->app->environment() !== 'production') {
	        $this->app->register(\Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class);
	    }
	    // ...
	}
```


## Installer le Plugin Laravel dans PhpStorm

* Dans PhpStorm : File / Settings / Browse Repository 
* Entrer "Laravel" dans la barre de recherche
* Sélectionner "Laravel Plugin"
* Installer
* Redémarrer PhpStorm
* Dans la bulle verte, en bas à droite de PhpStorm, cliquer sur "autoconfig"



# PhpStorm

## Augmenter la taille de police dans PhpStorm 

* Ctrl + Shift + a 
* Choisir "Increase font size" 

## Accéder au code de la page depuis le code d'une autre page

* "Ctrl + clic" sur le nom de la page 
* ou "Ctrl + b" sur le nom de la page  
