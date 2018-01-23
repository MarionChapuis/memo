# BDDLaravel

## Principe de base 

route -> controller -> vue 

## Se connecter à une BDD 

Modifier les éléments suivants du ".env" : 
* DB_DATABASE = nom BDD
* DB_USERNAME = nom utilisateur
* DB_PASSWORD = mot de passe

## Raw Sql Queries 

Ajouter des requêtes SQL dans notre controller 

```php 
$variable = DB::select('SELECT * FROM table WHERE id= ?', [variable remplaçant le ?]); 
return view ('mavue', ["nomVariable" => $variable]);
```


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



## Faire des liens avec ROUTE 

* On indique que l'on fait un lien avec la route "nomRoute" ayant pour paramètre "id" étant issue de l'objet $uneboisson->id

```php
<a href="{{ route('nomRoute', ['id'=>$uneBoisson->id]) }}">Texte</a>
```

## Asset : trouver le bon fichier

* Permet de trouver tout seul le bon fichier 
*Exemple :*
```php
<link href='{{asset("css/app.css")}}'>
```


## Donner une URL absolue 

```php
<a href="{{url('tableaubord')}}">
```



# Migrations

**Les migrations gérent le schéma de la BDD.**

* Les migrations sont dans le dossier : Database/Migrations
* Créer une migration et une table en ligne de commande : php artisan make:migration Nom_Migration --create=NomTable
* Dans le fichier de migration créé, renseigner la fonction "UP" avec les champs à créer
* Anticiper une erreur (clé trop longue) : App/Providers/AppServiceProvider.php 
* Dans la fonction boot(), ajouter : 
```php
use Illuminate\Support\Facades\Schema;
class AppServiceProvider extends ServiceProvider
{
	public function boot()
	{
	   Schema::defaultStringLength(191);
	}
}
``` 
* Pour obtenir la dernière version : php artisan migrate
* S'il y a une erreur, corriger l'erreur puis : php artisan migrate:fresh 

[Lien résolution de l'erreur](https://laravel-news.com/laravel-5-4-key-too-long-error)



# Modèles

**Un modèle permet d'interagir avec les tables.** 


## Créer un modèle 

* Créer un modèle avec la ligne de commande : php artisan make:model Nom_modèle
* Le fichier suivant est créé : App/Nom_modèle.php


## Ajouter un enregistrement 

* Lancer la ligne de commande : php artisan tinker
* Créer une instance de notre modèle (le modèle est une classe) : $instance = new App\Modèle(); 
	* On utilise App\ car le modèle indique "namepspace App;"
* Remplir l'enregistrement : $instance->attribut1 = "blablabla";
* Sauvegarder l'enregistrement : $instance->save(); 

Méthode avec "create" : 
* $boisson = App\Boisson::create(['name' => 'Café Long', 'price' => 80]);


## Indiquer les éléments modifiables 

Indiquer les éléments que l'on peut renseigner lors du remplissage de masse (création d'un enregistrement) sinon Laravel bloque le remplissage des champs.

* Dans le modèle créé, indiquer dans la classe les champs que l'on autorise à modifier 
```php
class Boisson extends Model
{
    //Préciser les champs que l'on a le droit de modifier 
    protected $fillable = ['name', 'price'];
}
```
* Redémarrer Tinker : php artisan tinker
* Méthode avec "create" : 
```php
$boisson = App\Boisson::create(['name' => 'Café Long', 'price' => 80]);
```


## Utiliser les méthodes de la classe Modèle 

* Trouver un enregistrement avec la méthode Static Find : App\NomModèle::find(n°);  
```php
App\Boisson::find(1);
=> App\Boisson {#808
     id: 1,
     name: "Café court",
     price: 50,
     created_at: "2018-01-23 13:24:53",
     updated_at: "2018-01-23 13:24:53",
   }
```


* Trouver un enregistrement avec la sécurité de retourner une erreur s'il n'existe pas : App\NomModèle::findOrFail(n°);
```
>>> App\Boisson::findOrFail(3)
Illuminate\Database\Eloquent\ModelNotFoundException with message 'No query results for model [Ap
p\Boisson] 3'
>>>
```


* Trouver un enregistrement avec un contenu précis : App\NomModèle::where('attribut' , 'est à égale à Blablabla')->get(); 
```
>>> App\Boisson::where('name', 'Café Court')->get();
=> Illuminate\Database\Eloquent\Collection {#808
     all: [
       App\Boisson {#812
         id: 1,
         name: "Café Court",
         price: 50,
         created_at: "2018-01-23 13:24:53",
         updated_at: "2018-01-23 13:29:50",
       },
     ],
   }
```

* Possible d'enchaîner les méthodes : App\NomModèle::where('attribut' , 'est à égale à Blablabla')->get()->first() ;

* Trouver un enregistrement et sélectionner les infos à afficher :  App\NomModèle::where('attribut', 'blabla')->select(['attribut1', 'attribut2'])->get();

* Le mettre dans un tableau : App\Boisson::where('name', 'Café Court')->select(['price'])->get()->toArray();

* Supprimer un enregistrement : delete() 
	* Stocker l'enregistrement dans une variable : $variable = App\NomModèle::find(1) ; 
	* Le supprimer : $variable->delete();

* Supprimer un enregistrement en utilisant l'id : destroy(id);

* Afficher tous les enregistrements : $variable = NomModèle::all(); 
	* Dans la vue : $variable->name;

* Trier les enregistrements : $variable = NomModèle::orderBy('attribut', 'asc ou desc')->get();


## Imposer une instance d'une classe en paramètre  

* Retourner une vue affichant les informations d'une boisson sélectionnée (par l'id)

```php
public function showBoissons($boisson)
{
	$drink = Boisson::find($id);
	return view('editBoissons', ["boisson" => $boisson]);
}
```

**Avec la magie :**

```php
public function showBoissons(Boisson $boisson)
{
	return view('editBoissons', ["boisson" => $boisson]);
}
```
