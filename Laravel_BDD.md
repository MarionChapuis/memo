# BDDLaravel

## Créer un Controller et l'ensemble de ses routes 

Créer un controller avec l'ensemble de ces méthodes à l'intérieur et toutes les routes associées (et nommées).
* lLgne de commande : php artisan make:controller NomController --resource
* Dans le fichier web : 
```php
Route::resource('ingredients', 'IngredientController') ; 
// ingredients : nom de la ressource 
// IngredientController : nom du controller
````

* Obtenir la liste des routes et leur nom : php artisan route:list

* Penser dans le controller à ajouter : use App\NomModel (ex App\Ingredient)
* Dans une vue insérer directement avec le nom de la route : 
```php
<a href="{{route('ingredients.index')}}"></a>
```


## Principe de base 

route -> controller -> vue 

## Se connecter à une BDD 

Modifier les éléments suivants du ".env" : 
* DB_DATABASE = nom BDD
* DB_USERNAME = nom utilisateur
* DB_PASSWORD = mot de passe

## Raw Sql Queries 

* Ajouter des requêtes SQL dans notre controller 

```php 
$variable = DB::select('SELECT * FROM table WHERE id= ?', [variable remplaçant le ?]); 
return view ('mavue', ["nomVariable" => $variable]);
```

* Avoir des paramètres non définis dans une requête
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


## Renommer une route 

Route::get('boissons/{id}', 'BoissonsController@showBoissons')->name('BoissonsShow'); //Je renomme la route 


## Avoir des paramètres dans une route

* Dans ma route : 
```php
Route::get('boissons/{id}', 'BoissonsController@showBoissons');
```


## Faire des liens href vers une ROUTE 

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
	* *exemple : php artisan make:migration create_boisson_table --create=boissons*
* Dans le fichier de migration créé, renseigner la fonction "UP" avec les champs à créer 
```php
class CreateBoissonTable extends Migration
{
    public function up()
    {
        Schema::create('boissons', function (Blueprint $table) {
            $table->increments('id');
            $table->string('name')->unique();
            $table->integer('price');
            $table->timestamps();
        });
    }
}
```


* Anticiper une erreur (clé trop longue), dans le fichier : App/Providers/AppServiceProvider.php 
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


## Créer un modèle & sa migration

* Créer un modèle avec la ligne de commande : php artisan make:model Nom_modèle
	* Ou *Créer un modèle avec la ligne de commande et sa migration : php artisan make:model Nom_modèle -m*
* Le fichier suivant est créé : App/Nom_modèle.php
* Dans le fichier de migration créé (Database/Migrations/create_nomTable_table), renseigner la fonction "UP" avec les champs à créer dans la table
```php
class CreateBoissonTable extends Migration
{
    public function up()
    {
        Schema::create('boissons', function (Blueprint $table) {
            $table->increments('id');
            $table->string('name')->unique();
            $table->integer('price');
            $table->timestamps();
        });
    }
}
```

* Dans le modèle créé, indiquer dans la classe les champs que l'on autorise à modifier 
```php
class Boisson extends Model
{
    //Préciser les champs que l'on a le droit de modifier 
    protected $fillable = ['name', 'price'];
}
```
* Finaliser et créer la table : php artisan migrate


A noter, dans Bash, il est possible d'utiliser Tinker pour dialoguer avec la BDD - ligne de commande : php artisan tinker


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


# Synthèse des méthodes 

Les méthodes, souvent héritées de Model, peuvent être enchaînées : where('attribut', '= à')->select()->...


| Méthodes | Définition | Exemple 
|:-------:|:-------:|:-------:|
| new NomClass(); | Créer une instance d'une classe | $instance = new NomClass();
| $instance->attribut=""; | Modifier la valeur d'un attribut | $instance->attribut = "bla";
| save() | Méthode permettant d'enregistrer l'instance | $instance->save();
| create(array) | Méthode permettant de passer en paramètre un tableau pour renseigner les attributs d'une instance | $boisson = App\Boisson::create(['name' => 'Café Long', 'price' => 80]);
| find($paramètre) | Méthode permettant de trouver un enregistrement | NomClasse::find($id); 
| findOrFail($paramètre) | Méthode permettant de trouver un enregistrement et retourner une erreur s'il n'existe pas | NomClasse::findOrFail($id); 
| where('attribut' , '= à')->get(); | Where permet de trouver un enregistrement avec un contenu spécifique et de le récupèrer grâce à get() | NomClasse::where('name', 'toto')->get()
| select([attributs]) | Sélectionner les infos à afficher | NomClass::where(..)->select(['attribut1','attribut2'])->get() ;
| toArray() | Obtenir le résultat dans un tableau | NomClasse::where(..)->get()->toArray() ;
| delete() | Supprimer un enregistrement | $instance->delete() ;
| destro(id) | Supprimer un enregistrement en le sélectionnant | $instance->destroy(id) 
| all() | Afficher tous les engistrements | $instance = NomClass::all() ; (Dans la vue : $instance->attribut1)
| orderBy('attribut', 'asc ou desc') | Trier les enregistrements | NomClass::order('name', 'desc')->get() ;



## Imposer une instance d'une classe en paramètre  

* Retourner une vue affichant les informations d'une boisson sélectionnée (par l'id)

```php
public function showBoissons($id)
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
* $boisson est une instance de la classe Boisson. Pour fonctionner il se base sur le champ "id"

*A noter, s'il n'y a pas de champs "id" dans notre table, il faut indiquer dans le model le champs servant d'id* :
```php
class Boisson extends Models
{
    public function getRouteKeyName()
    {
        return 'code_boisson';
    }
}
```


## Mise à jour des données avec le Model

### Ajouter des données 

* Ajouter en haut de la page le lien pour avoir accès à Request : use Illuminate\Http\Request;
* Ajouter une méthode Store dans le Controller 
```php
public function store(Request $request)
{
	// Je récupère les infos de mon formulaire
	$data = 
	[
        'name'  => $request->input('name'),
        'price'   => $request->input('price'),
    ];

	// J'ajoute dans ma BDD les infos de mon formulaire
      $boisson=Boisson::create($data);
        
    // //J'affiche ma liste des boissons 
    return redirect()->route('Drinks');   //sans utiliser une route renommée : return redirect('boissons');
} 
``` 

* Formulaire d'ajout :
```php
<form action="{{route('ingredients.store')}}" class="form-group well col-md-offset-2 col-md-8" method="post">
    {{ csrf_field() }}
    <label class="col-md-4" for="name">Nom Ingrédient</label>
    <input class="col-md-8" name="name" required="required" type="text">
    <br><br>
    <label class="col-md-4" for="stock">Stock</label>
    <input class="col-md-8" type="text" name="stock" required="required">
    <br><br>
    <button type="submit" class="btn btn-lg btn-primary">Ajouter</button>
</form>
```


### Modifier des données 

* Ajouter en haut de la page le lien pour avoir accès à Request : use Illuminate\Http\Request;
* Ajouter une méthode Publish dans le Controller 
```php
public function update(Request $request, $boisson)
{
	//Je récupère les données de mon formulaire
	$data = 
	[
	'name'  => $request->input('name'),
	'price' => $request->input('price'),
	];
	
	// Je met à jour ma boisson avec les données de mon formulaire
	$boisson::update($data);

	// //J'affiche ma liste des boissons 
	return redirect()->route('Drinks');
}
``` 

* Ajouter dans le formulaire le Input magique (sinon ça ne marche pas )
```html
<input type="hidden" name="_method" value="put">
```


### Supprimer des données 

* Ajouter en haut de la page le lien pour avoir accès à Request : use Illuminate\Http\Request;
* Ajouter une méthode Delete dans le Controller 
```php
public function deleteDrink(Boisson $boisson)
{
	$boisson->delete();
	return redirect()->route('Drinks');
}
``` 

* Ajouter dans le formulaire le Input magique (sinon ça ne marche pas )
```html
<input type="hidden" name="_method" value="delete">
```

*exemple de bouton pour supprimer :*
```php
<form method="post">
	{{ csrf_field() }}
	<input type="hidden" name="_method" value="delete">
	<button type="submit" class="btn btn-lg btn-warning col-md-offset-1 col-md-3">Supprimer</button>
</form>
```




# Relations entre modèles 


## Relation One to One : hasOne et belongsTo

Relation : un utilisateur a un téléphone

* Dans l'un des Model on ajoute une méthode portant le nom de l'autre Model 
```php
class User extends Model
{
	public function phone()
	{
		return $this->hasOne('App\Phone');
	}
}
```
	* hasOne : nom de la relation
	* App\Phone : lien vers le 2ème Model

* Eloquent crée automatiquement la clé étrangère dans le 2ème Model 
* Dans le 2ème Model on crée : belongsTo
```php
class Phone extends Model 
{ 
	public function user()
	{
		return $this->belongsTo('App\Phone');
	}
} 
```

* Dans le fichier de migration (create_nomModel_table), ajouter l'index : nomTable2_id
```php 
class CreatePhoneTable extends Migration
{
    public function up()
    {
        Schema::create('ventes', function (Blueprint $table) {
            $table->increments('id');
            $table->integer('user_id')->unsigned()->index(); //unsigned : valeur positive
            $table->timestamps();
        });
    }
}
```


## Relation One To Many : hasMany et belongsTo

Relation une Boisson a plusieurs Ventes 

* Dans le Model Boisson, on crée la méthode "ventes" 
```php
class Boisson extends Model
{
	public function ventes()
	{
		return $this->hasMany('App\Vente');
	}
}
```

* Dans le Model Vente, on crée la méthode "boisson"
```php
class Vente extends Model
{
	public function boisson()
	{
		return $this->belongsTo('App\Boisson');
	}
}
```

* On crée la clé étrangère et les champs dans le fichier de migration de Ventes
```php
class CreateVentesTable extends Migration
{
    public function up()
    {
        Schema::create('ventes', function (Blueprint $table) {
            $table->increments('id');
            $table->integer('nbSugar');
            $table->integer('boisson_id')->unsigned();
            $table->foreign('boisson_id')->references('id')->on('boissons');
            $table->timestamps();
        });
    }
}
```

* Dans les Models, on précise les champs que l'on pourra modifier 
```php
class Vente extends Model
{
    //Préciser les champs que l'on peut modifier 
    protected $fillable = ['nbSugar', 'boisson_id'];
}
```

* Faire la migration en ligne de commande : php artisan migrate


## Relation Many To Many : belongsToMany

Relation entre Boisson et Ingredient 

* Dans le Model Boisson, on crée la méthode "ingredients" et les champs qu'on autorise à modifier
* Pour tous les champs autres que "boisson_id" et "ingredient_id", il faut les préciser dans les 2 Models : "withPivot"
```php
class Boisson extends Model
{
    //Préciser les champs que l'on a le droit de modifier 
    protected $fillable = ['name', 'price'];

    public function ingredients()
    {
    	return $this->belongsToMany('App\Ingredient')->withPivot('quantity');
    }
}
```

* Dans le Model Ingredient, on crée la méthode "boissons" et les champs qu'on autorise à modifier
```php
class Ingredient extends Model
{
    protected $fillable = ['name', 'stock'];

    public function boissons()
    {
    	return $this->belongsToMany('App\Boisson')->withPivot('quantity');
    }
}
```

* Faire une migration pour créer la table de liaison : elle se nomme nomModel1_nomModel2 (par ordre alphabétique)
```
$ php artisan make:migration create_boisson_ingredient_table
```

* Dans le fichier de migration qui vient d'être créé, on précise les champs dans la table de liaison (clé primaire & étrangère)
```php
class CreateBoissonIngredientTable extends Migration
{
    public function up()
    {
        Schema::create('boisson_ingredient', function (Blueprint $table) 
        {
            $table->integer('boisson_id');
            $table->integer('ingredient_id');
            $table->primary(['boisson_id','ingredient_id']);  //clé primaire : couple
            $table->foreign('boisson_id')->references('id')->on('boissons'); //clé étrangère
            $table->foreign('ingredient_id')->references('id')->on('ingredients'); //clé étrangère
            $table->integer('quantity');
            $table->timestamps();
        });
    }
}
```

* Faire la migration en ligne de commande : php artisan migrate

### Accèder aux éléments de la table de liaison

**La table de liaison est connu sous le nom de "pivot", qui est un objet.**

* Fonction permettant de récupèrer la recette d'une boisson :
```php
public function showBoissons(Boisson $boisson) //je demande un paramètre de la classe Boisson (cherche par défaut l'id)
    {
        //Récupèrer les ingrédients d'une boisson
        $recette = $boisson->ingredients;

        //Retourner la vue avec les données 
        return view('editBoissons', ["boisson" => $boisson, "recette"=> $recette]);
    }
```

* Dans la vue, pour afficher tous les ingrédients et les quantités (nb doses) :
```php
@foreach ($recette as $unIng)
    <tr>
        <td>{{ $unIng->name }}</td> //On récupère le nom de l'ingrédient dans la table ingrédient
        <td>{{ $unIng->pivot->quantity }}</td> //On récupère la quantité dans la table Pivot (boisson_ingredient)
    </tr>
@endforeach
```
