# LARAVEL 5.5

## Faire le lien avec Bootstrap 

Ajouter la ligne dans le template : 
```html
<link rel="stylesheet" href="{{('css/app.css')}}">
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

Dans un premier temps on dit qu’on veut utiliser le template avec @extends et le nom du template « template ». Ensuite on remplit les zones prévues dans le template grâce à la syntaxe @section en précisant le nom de l’emplacement et en fermant avec @endsection. Voici un schéma pour bien visualiser tout ça avec les articles :

![Schéma Template](https://raw.githubusercontent.com/MarionChapuis/memo/master/principe_template.jpg)

