# Formulaire Laravel


## Template : head 

* Mettre la balise : **<meta name="csrf-token" content="{{ csrf_token() }}">**
```php 
<head>
    <meta charset="utf-8">
    <meta name="csrf-token" content="{{ csrf_token() }}">
</head>
```


## Le formulaire 

* Avoir une vue : formulaire.blade.php
* Ajouter dans le formulaire la protection : {{ csrf_field}}
```php
	<form class="" action="/user" method="post">
        {{ csrf_field() }}
```

  
## La vue d'affichage

* Avoir une vue qui affiche les résultats du formulaire : result.blade.php
* Afficher une valeur du formulaire : {{ $user['firstname'] }}
```php 
<p>valeur : <b>{{ $user['firstname'] }}</b></p>
```


## Le controller

* Créer un controller avec la ligne de commande : **php artisan make::controller NomController -r**
* Dans la fonction "create" 
```php
public function create()
{
    return view('user.formulaire');
}
```

* Dans la fonction "store"
```php 
public function store(Request $request)
{
    $data = [
	   'user' => [
			'firstname'  => $request->input('firstname'),
			'lastname'   => $request->input('lastname'),
         ],
    ];

    return view('user.result', $data);

}
```


## La route 

Il existe 2 routes : 
* Pour afficher le formulaire : **GET** 
* Pour soumettre le formulaire et afficher la vue : **POST**

```php
Route::get('/user/create', 'UserController@create');
Route::post('/user', 'UserController@store');
```


## Architecture 


