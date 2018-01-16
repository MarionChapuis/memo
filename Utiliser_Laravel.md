# LARAVEL 5.5


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


## Faire le lien avec Bootstrap 

Ajouter la ligne dans le template : 
```html
<link rel="stylesheet" href="{{('css/app.css')}}">
```

## Faire le lien avec notre css : 
```html
<link rel="stylesheet" href="{{('css/style.css')}}">
```

## Créer une vue 

* Ajouter une vue dans "Resources / Views "
* Nommer la vue "NomVue.blade.php"
* Dans "Routes / web.php ", créer l'URL avec le code suivant 
```php
Route::get('NomVue', function () {
    return view('NomVue');
});
```

* La vue est maintenant disponible avec l'URL ".../NomVue" 



## Ajouter des liens de navigation entre les pages

* Ajouter dans le code : 
```html 
<a href="NomVue">Nom de la vue</a>
```



## Blade Templates

### Syntaxes de bases 

##### Ouvrir des balises Blade :

Tout ce qui se trouve entre les doubles accolades est interprété comme du code PHP.
**<?=**  équivaut dans Blade à  **{{**


Par exemple : 
```php
{{ "Bonjour" }}
```

Equivaut à :
```php
<?= "Bonjour" ?>
```


##### Ajouter du code html

Par exemple, pour afficher un titre H2 : 
```php
{!! "<h2>Bonjour</h2>" !!}
```


### Templates 

Le templating permet de factoriser le code et éviter la redondance de code. 
Par exemple, on peut créer un template d'une vue qui sera utilisée dans différentes pages de notre site.

*Exemple d'un template*
```html
<!doctype html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>@yield('titre')</title>
</head>
<body>
    @yield('contenu')
</body>
</html>
```

*Exemple d'application du template dans une autre page*
```html
@extends('NomTemplate')

@section('titre')
	Mon Titre
@endsection

@section('contenu')
	<p>Mon paragrapge blablabla </p>
@endsection
```

Exemple
Dans un premier temps on dit qu’on veut utiliser le template avec @extends et le nom du template « template ». Ensuite on remplit les zones prévues dans le template grâce à la syntaxe @section en précisant le nom de l’emplacement et en fermant avec @endsection. Voici un schéma pour bien visualiser tout ça avec les articles :

![Schéma Template](https://raw.githubusercontent.com/MarionChapuis/memo/master/principe_template.jpg)

**Il est possible d'utiliser @include pour inclure un template (sans passage dynamique dans le template)**
*Exemple d'application de la commande @include*
```html
@include('templates/MonTemplate')
```



Nom d'un controller : **N**om**C**ontroller (commence par une majuscule)

```php
class NomController extends Controller
{
	public function() {
		return view('maVue');
	}
}
```


Le fichier "MonController.php" est à placer dans le dossier "App / Http / Controllers"
