# BDDLaravel

## Principe de base 

route -> controller -> vue 


## Renommer une route 

Route::get('boissons/{id}', 'BoissonsController@showBoissons')->name('BoissonsShow'); //Je renomme la route 


## Avoir des paramètres dans une route

```php
public function showBoissons($id) 
{
    $drink = DB::select('SELECT * from drink where id=?',[$id]);
    return view('editBoissons', ["boisson" => $drink[0]])
}
```

* ? est remplacé par le 2ème paramètre de la fonction selection [$id]
* $drink[0] : car le tableau contient un seul objet issu de la requête
* pour appeler les infos : $boisson->name

Dans ma route : 

```php
Route::get('boissons/{id}', 'BoissonsController@showBoissons');
```

{$id} est un paramètre


## Faire des liens avec ROUTE 

* On indique que on fait un lien avec la route "nomRoute" ayant pour paramètre "id" étant issue de l'objet $uneboisson->id

```php
<a href="{{ route('nomRoute', ['id'=>$uneBoisson->id]) }}">Texte</a>
```

## Asset 

* Permet de trouver tout seul le bon fichier 
*Exemple :*
```php
<link href='{{asset("css/app.css")}}'>
```


## Donner une URL absolue 

```php
<a href="{{url('tableaubord')}}">
```
