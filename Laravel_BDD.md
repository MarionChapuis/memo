# BDDLaravel

## Créer un Controller et l'ensemble de ses routes 

Créer un controller avec l'ensemble de ces méthodes à l'intérieur et toutes les routes associées (et nommées).
* Ligne de commande : php artisan make:controller NomController --resource
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
* S'il y a une erreur, corriger l'erreur puis : php artisan migrate:fresh (permet de tout efface dans les tables)

[Lien résolution de l'erreur](https://laravel-news.com/laravel-5-4-key-too-long-error)

## Commande php artisan migrate 

| Commande | Action |
| :-------:|:-------:|
| php artisan migrate | Actualiser notre BDD avec les dernières modifications
| php artisan migrate:rollback | Supprimer la dernière migration (voir dans la table "migrations" de la BDD pour savoir quels seront les modifications supprimées)
|  


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

## Pré-remplir la BDD avec des données définies 

* Renseigner le fichier DatabaseSeeder.php dans Database/Seeds
```php
use App\User;

public function run()
{
    // $this->call(UsersTableSeeder::class);
    User::create(
        [
            'id'       => 1,
            'name'     => 'Guest',
            'email'    => '',
            'password' => '',
            'role'     => 'guest',
        ]
    );
    User::create(
        [
            'id'       => 2,
            'name'     => 'Admin',
            'email'    => 'admin@example.com',
            'password' => 'MonSuperMotDePasse',
            'role'     => 'guest',
        ]
    );
}
```

* En ligne de commande 
```
php artisan db:seed
```

## Encrypter les password 

Lorsque les mots de passe sont directement renseignés dans la BDD (via PhpMyAdmin par exemple), le mot de passe est visible. 

Il faut donc encrypter aussi ces mots de passe.

* Ajouter une fonction dans le Model "User.php"
```
public function setPasswordAttribute($password)
    {
        $this->attributes['password'] = bcrypt($password);
    }
```

* Modifier le fichier "RegistrerController.php"
```
protected function create(array $data)
    {
        return User::create([
            'name' => $data['name'],
            'email' => $data['email'],
            'password' => $data['password'], //j'ai supprimé le "bcrypt"
        ]);
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
| first() | Récupérer le premier élément d'une collection, à utiliser quand la collection contient un seul élément | NomClasse::where('name', 'sucre')->first();
| isNotEmpty() | Tester si une Collection est vide (retourne true ou false) | $instance->isNotEmpty() ;


[Documentation sur les méthodes Laravel pour les collections](https://laravel.com/docs/5.6/collections#available-methods)



**Créer un champs temporaire dans un objet** 
* Dans le Controller 
```php
public function index()
{
    $boisson->dispo = true;
}
```
* Dans la Vue 
```php
@if ($boisson->dispo === true)
//...
@endif
```

**Quelques calculs sur les données**
* Compter des données
```php
$user->ventes->count(); // Compte le nombre de ventes d'un utilisateur
```
* Calculer une somme
```php
number_format($user->ventes->sum('price')/100,2); // Calculer la somme des prix de ventes d'un utilisateur 
// number_format(number, nb décimal) permet de formater le résultat
``` 


## Imposer une instance d'une classe en paramètre  

Typer les données en imposant une instance d'une classe en paramètre d'une fonction.

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

* Ajouter dans le formulaire la méthode suivante (sinon ça ne marche pas )
```html
<form>
{{csrf_method('delete')}}
</form>
```

*La méthode ci-dessous fonctionne aussi mais il vaut mieux utiliser la précédente*
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

### Accéder aux données 

Je souhaite afficher mes ventes et remplacer "boisson_id" par le nom de la boisson (dispo dans le Model Boisson). 
J'utilise la relation entre les modèles.

* Dans mon VenteController, je retourne l'ensemble des ventes : 
```php
public function index()
    {
        $data =
            [
                'ventes' => Vente::orderBy('id')->get(),
            ];
        return view('ventes.list', $data);
    }
```

* Dans ma vue, je réalise une boucle pour afficher chaque vente et j'accède au nom de ma boisson
```php
@foreach ($ventes as $vente)
    <tr>
        <td>{{ $vente->id }}</td>
        <td>{{ $vente->created_at }}</td>
        <td>{{ $vente->boisson->name }}</td>
        <td>{{ $vente->nbSugar }}</td>
    </tr>
@endforeach
```

* **$vente->boisson->name** : je peux accèder à ma table Boisson contenant le nom


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


### Ajouter un élément dans la table de liaison : ATTACH

Attach permet "d'attacher" un élément à un autre. Par exemple, 

Dans le controller, créer une méthode permettant d'ajouter une recette pour la boisson sélectionnée 

```
public function addRecipe(Request $request, Boisson $boisson)
{
    // Je récupère les infos de mon formulaire
    $data = 
    [
        'ingredient_id'  => $request->input('ingredient_id'),
        'quantity'   => $request->input('quantity'),
    ];

    //J'ajoute l'ingrédient dans ma recette
    $boisson->ingredients()->attach($data['ingredient_id'], ['quantity'=>$data['quantity']]);

    return redirect()->route('FormulaireRecette', ['boisson'=>$boisson]);
}
```

**Explications** : 
* la table de liaison contient les champs suivants : boisson_id , ingredient_id et quantity
* boisson_id est récupéré par le paramètre de la méthode (Boisson $boisson)
* ingredient_id et quantity sont récupérés dans le formulaire 
* les 2 champs sont ajoutés à la table via attach(ingredient_id, [AutreChampsPivot => valeur de ce champs])
et attaché avec "attach"

**Les routes** : 
* Route pour afficher le formulaire 
```
Route::get('boissons/{boisson}/recette', 'BoissonsController@formRecipe')->name('FormulaireRecette');
```
* Route pour ajouter un ingrédient 
```
Route::post('boissons/{boisson}/recette', 'BoissonsController@addRecipe')->name('ajoutRecette');
```



### Supprimer un élément dans la table de liaison : DETACH 

Detach permet de "détacher" un élément d'un autre. Par exemple, détacher un ingrédient d'une boisson (l'ingrédient ne fait donc plus partie de la recette).

Dans le controller, créer une méthode permettant de supprimer un ingrédient pour la boisson sélectionnée 
```
public function deleteIng(Request $request, Boisson $boisson)
{
    //Récupérer l'id_ingrédient via le bouton sélectionné 
    $ingredient= $request->input('ingredient');

    $boisson->ingredients()->detach($ingredient);
    return redirect()->route('FormulaireRecette', ['boisson'=>$boisson]);
}
```

Dans la vue, créer un bouton dans un tableau permettant de détacher l'ingrédient de la recette 
```
<form method="post">
{{ csrf_field() }}
    <table class="table table-hover table-bordered tableRecette">
        <tr>
        <th>Ingrédient</th>
        <th>Dose</th>
        <th>Supprimer</th>
        </tr>
    @foreach ($recette as $unIng)
        <tr>
            <td>{{ $unIng->name }}</td>
            <td>{{ $unIng->pivot->quantity }}</td>
            <td> 
                //Créer un input caché avec la méthode "delete"
                <input type="hidden" name="_method" value="delete">
                // Créer un bouton type submit ayant comme valeur l'id de l'ingrédient et comme nom "ingredient"
                <button type="submit" value="{{ $unIng->id}}" name="ingredient" class="btn btn-sm btn-danger">Supprimer</button>
            </td>
        </tr>
    @endforeach
    </table>
</form>
```

**Les routes** : 
* Route pour afficher le formulaire 
```
Route::get('boissons/{boisson}/recette', 'BoissonsController@formRecipe')->name('FormulaireRecette');
```
* Route pour supprimer un ingrédient 
```
Route::delete('boissons/{boisson}/recette', 'BoissonsController@deleteIng')->name("IngRecipeDelete");
```
 

**Attention avec les BDD de type InnoDB, il n'est pas possible de supprimer un élément ayant des relations**

Par exemple, si l'on souhaite supprimer une boisson qui a une recette (donc des liens avec des ingrédients), il faut d'abord casser les liaisons pour supprimer la boisson. 

```php
if ($boisson->ingredients->count() >0) //Si la boisson a des ingrédients liés
{
    foreach ($boisson->ingredients as $ingredient) 
    {
        $boisson->ingredients()->detach($ingredient); //détacher chaque ingrédient
    }
}
$boisson->delete();
```


# Messages flash 

## Etape 1 : Créer une vue flash-message.blade.php 

```
@if ($message = Session::get('success'))
<div class="alert alert-success alert-block">
    <button type="button" class="close" data-dismiss="alert">×</button> 
        <strong>{!! $message !!}</strong>
</div>
@endif


@if ($message = Session::get('error'))
<div class="alert alert-danger alert-block">
    <button type="button" class="close" data-dismiss="alert">×</button> 
        <strong>{!! $message !!}</strong>
</div>
@endif


@if ($message = Session::get('warning'))
<div class="alert alert-warning alert-block">
    <button type="button" class="close" data-dismiss="alert">×</button> 
    <strong>{!! $message !!}</strong>
</div>
@endif


@if ($message = Session::get('info'))
<div class="alert alert-info alert-block">
    <button type="button" class="close" data-dismiss="alert">×</button> 
    <strong>{!! $message !!}</strong>
</div>
@endif


@if ($errors->any())
<div class="alert alert-danger">
    <button type="button" class="close" data-dismiss="alert">×</button> 
    Please check the form below for errors
</div>
@endif
```

## Etape 2 : Inclure la vue dans le template Structure

Pour que le message puisse s'afficher dans toutes les pages

```php 
<div class="content">
    <div class="title m-b-md">
    @yield('TitlePageName')
    </div>
    @include ('flash-message')
    @yield('content')
</div>
```

## Etape 3 : afficher le message 

Dans la méthode à l'intérieur du controller :
* Paramètrer le message : with()
* Renvoyer la même page : back()

```php
public function destroy(Ingredient $ingredient)
{
    if ($ingredient->boissons->count()>0) // Si l'ingrédient est associé à au moins une boisson
    {
        $boissons = $ingredient->boissons;
        $liste='';
        foreach($boissons as $boisson)
        {
            $liste .= "<li> ".$boisson->name. " (prix : " . $boisson->price/100 . " €, id : ". $boisson->id. " )</li>";
        }

        $informations = "Impossible de supprimer cet ingrédient car il est associé au(x) boisson(s) suivante(s) : ".$liste;
        
        // Revenir sur la même page en affichant le message type "error"
        return back()->with("error", $informations);
    }
    
    // Dans les autres cas, supprimer l'ingrédient
    $ingredient->delete();

    //Direction la route nommée avec le message type "info"
    return redirect()->route('ingredients.index')->with("info", "L'ingrédient ".$ingredient->name ." a bien été supprimé");
}
```

**Pour pouvoir ajouter des balises HTML dans le message** : 
* Dans le fichier "flash-message.blade.php" les messages sont affichés via : {{ $message }}
* Les {{ }} ne permettent pas d'utiliser un message avec des balises HTML à l'intérieur 
* Modifier les {{ }} en {!! !!} pour pouvoir ajouter des balises HTML

*Exemple:*
```php 
@if ($message = Session::get('error'))
<div class="alert alert-danger alert-block">
    <button type="button" class="close" data-dismiss="alert">×</button> 
        <strong>{!! $message !!}</strong> // par défaut : {{ $message }}
</div>
@endif
```


# Authenfication 

Laravel contient déjà une partie authentification permettant de se connecter, déconnecter, enregistrer et même envoyer un email lors de la perte du mot de passe.

## Créer les routes et vues 

Pour créer automatiquement les routes et vues, lancer la commande suivante dans le Bash : 
```
php artisan make:auth
```

Pour avoir la liste des routes : 
```
php artisan route:list
```

Dans le fichier web, les routes suivantes sont crées : 
```
Auth::routes();
Route::get('/home', 'HomeController@index')->name('home');
```

* Il faut donc modifier le "/home" en /
* En cas de problème de redirection : checker le HomeController : 
```php
public function index()
{
    return view('tableaubord'); //choisir la bonne vue à retourner
}
```



## Protéger les routes 

Pour que les utilisateurs qui ne sont pas authentifiés ne puissent pas accéder au site, il faut protéger les routes.

Ajouter à la fin de toutes les routes le **Middleware** : 
```php
Route::get('ventes', 'VentesController@listeVentes')->middleware('auth');
```

Si l'on entre l'URL "machine/ventes" on sera redirigé vers la page Login.


## Récupérer les informations Utilisateurs 

**Ajouter dans le Controller le lien :**
```
use Illuminate\Support\Facades\Auth;
```

* Vérifier si l'utilisateur est connecté :
```
Auth::check(); // Retourne True or False
```
* Récupérer l'id de l'utilisateur :
```
Auth::id();
```
* Récupérer un objet avec les données de l'utilisateur 
```
Auth::user();
```




## Infos 

Liste des fichiers créés automatiquement :
* Dans le fichier "web.php", le code suivant a été ajouté pour créer l'ensemble des routes : 
```
Auth::routes();
Route::get('/home', 'HomeController@index')->name('home');
```
* Vue : 'home'
* Dans les "Views" il y a 2 nouveaux dossiers : Auth et Layouts
* Dossier "Auth" :
    * Dossier Passwords contenant les vues 'email' et 'reset'
    * Vue 'Login'
    * Vue 'Register'
* Dossier "Layouts" :
    * Vue 'app' : template avec barre de navigation et déconnexion 
* Controller : HomeController (App\Http\Controllers)
* ...


# Profils utilisateurs 

## Vérifier si l'utilisateur est connecté

Pour vérifier si l'utilisateur est connecté : 
* Dans un Controller :
```php
Auth::check();
```
* Dans une Vue :
```php 
Illuminate\Support\Facades\Auth::check();
```

Exemple : 
* Dans un Controller :
```php
use Illuminate\Support\Facades\Auth;

public function index()
{
    if (Auth::check()) {
        $data =
        [
        'ventes' => Vente::orderBy('id')->get(),
        ];
        return view('ventes.list', $data);
    }
    else
    {
        return redirect()->route('machine');
    }
}
```
* Dans une Vue :
```php
<ul class="nav navbar-nav">
    <li><a href="{{route('machine')}}">Machine</a></li>

    @if (Illuminate\Support\Facades\Auth::check())
        <li><a href="{{url('boissons')}}">Boissons</a></li>
        <li><a href="{{url('triBoissons')}}">Boissons triées</a></li>
        <li><a href="{{route('ingredients.index')}}">Ingrédients</a></li>
        <li><a href="{{url('monnayeur')}}">Monnayeur</a></li>
        <li><a href="{{route('ventes.index')}}">Ventes</a></li>
    @endif
</ul>
```


# Authorization 

Donner le droit d'accès à des routes selon le profil de l'utilisateur.


## MIDDLEWARE

Un Middleware est entre le Routing et le Controller. Il peut donc refuser l'accès à un Controller.

#### Créer un Middleware

* Ligne de commande 
```
php artisan make:middleware NomMiddleware
```
* Emplacement : App\Http\Middleware

**Exemple**
```
php artisan make:middleware CheckRole
```


#### Définir la méthode 'handle'

Lors de la création du Middleware, une méthode 'handle' est automatiquement créée. 

**Exemple** 

Si l'utilisateur n'est pas connecté comme 'admin' il est automatiquement redirigé vers la page d'accueil

```php
class CheckRole
{
    public function handle($request, Closure $next)
    {
        // Si l'utilisateur n'est pas connecté avec un rôle 'admin', retour vers la page d'accueil
        if ($request->user()->role != 'admin') {
            return redirect('/');
        }
        // Sinon la demande est acceptée : la requête URL est validée
        return $next($request);
    }
}
```

* Request : correspond à la requête URL 
* next : permet l'affichage du résultat de l'URL (prochaine étape)

#### Enregistrer le Middleware dans Kernel.php

Le fichier Kernel regroupe l'ensemble des Middlewares. Il faut donc ajouter notre nouveau Middleware.

* Enregistrer le Middleware 
```php
protected $routeMiddleware = 
[
    'auth'       => \Illuminate\Auth\Middleware\Authenticate::class,
    'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
    'bindings'   => \Illuminate\Routing\Middleware\SubstituteBindings::class,
    'can'        => \Illuminate\Auth\Middleware\Authorize::class,
    'guest'      => \App\Http\Middleware\RedirectIfAuthenticated::class,
    'throttle'   => \Illuminate\Routing\Middleware\ThrottleRequests::class,
    'role'       => \App\Http\Middleware\CheckRole::class, // 'role' a été ajouté et fait le lien avec le Middleware 'CheckRole'
]
```

#### Utiliser le Middleware pour protéger une route 

**Exemple**
```php
// Route pour afficher la liste des boissons 
Route::get('boissons', 'BoissonsController@listeBoissons')->name("Drinks")->middleware(['auth', 'role']);
```

* 'auth' : accès possible uniquement par les utilisateurs connectés
* 'role' : accès possible uniquement par les utilisateurs avec un profil 'admin' (selon le Middleware)

**Il est possible, d'ajouter des paramètres à 'role'**
```php
Route::get('boissons', 'BoissonsController@listeBoissons')->name("Drinks")->middleware(['auth', 'role:admin']); 
```

```php
public function handle($request, Closure $next, $role)
    {
        // Si l'utilisateur n'est pas connecté avec un rôle 'admin', retour vers la page d'accueil
        if ($request->user()->role != $role) {
            return redirect('/');
        }
        // Sinon la demande est acceptée : la requête URL est validée
        return $next($request);
    }
```

## Retourner une page d'erreur 

Lorsque l'utilisateur n'a pas les droits d'accès à une page, retourner une page d'erreur. 
Ainsi, impossible de savoir si la page existe ou non. 

```php 
public function index()
{
    if (User::check())
    {
        ....
    }
    // Retourner une page d'erreur s'il n'est pas connecté
    return abort(404); // n° de la page d'erreur : 404, 501 ... 
}

```

## GATES 



## POLICIES


# Validation de formulaire 



# JAVASCRIPT & PHP 

## Placer les fichiers JS & Images

Les fichiers JS et images sont respectivement à placer dans les dossiers suivants : 
* public/js
* public/images 

## Données PHP connues par JS 

Une solution provisoire pour que JavaScript connaisse des données PHP.

* Dans la vue PHP, ajouter une balise script 
```php
<script> valeurMaxStock ={{$maxSucre}}</script>
```
**Exemple** :
* valeurMaxStock sera utilisée dans le JS 
* $maxSucre est une variable connue par la vue PHP



# Quelques petites bouts de codes

### Formulaire avec des images à cliquer 

Avoir un formulaire caché permettant de cliquer sur une image pour la sélectionner 

* Dans le CSS :
```css
label > input{ /* HIDE RADIO */
    visibility: hidden; /* Makes input not-clickable */
    position: absolute; /* Remove input from document flow */
}
label > input + img{ /* IMAGE STYLES */
    cursor:pointer;
    border:2px solid transparent;
}
label > input:checked + img { /* (RADIO CHECKED) IMAGE STYLES */
    background-color: rgba(173,255,47,0.51);
    border-radius : 20px;
}
```

* Dans la Vue Blade 
```php
<table class="tableBoissons table-responsive">
@foreach ($drinks as $uneBoisson)
{{--Si la boisson est activée et que les stocks sont suffisants --}}
@if ($uneBoisson->active === 1 && $uneBoisson->dispo())
<tr>
<td>
<label>
<input type="radio" name="boisson_id" value="{{$uneBoisson->id}}" required>
<img class="petiteTasse" id="petiteTasse" src="image_machine/Vue1-assets/tasse.png" prixBoisson="{{$uneBoisson->price}}">
</label>
</td>
<td>{{ $uneBoisson->name }}</td>
<td class="droite price{{$uneBoisson->id}}">{{ number_format($uneBoisson->price/100,2) }}€</td>
</tr>
@endif
@endforeach
</table>
```

* Récupèrer l'info "prixBoisson" : il est possible d'ajouter un attribut à une image par exemple, pour récupérer une info dans le JS
```javascript
let prixBoisson = $(this).attr('prixBoisson'); //je récupère le prix de la boisson sélectionnée
```

### Ajouter du son 

* Dans la vue Blade, ajouter une balise script contenant la librairie Jquery permettant l'ajout de piste audio
```php
<script src='https://cdn.rawgit.com/admsev/jquery-play-sound/master/jquery.playSound.js'></script>
```

* Dans le script JavaScript, ajouter le fichier audio (à noter le dossier Audio est à placer dans Public)
```Javascript
$('.bouton').click(function(){
    $.playSound('audio/donald.mp3');
    });
```


### Bouton 'activer / désactiver'

* Dans un formulaire, ajouter une checkbox 
```php
<label class="switch col-md-8"> //La classe Switch est une classe Bootstrap
    <input type="checkbox" name="active" value="1">
    <span class="slider round"></span> // La classe Slider Round est une classe Bootstrap
</label>
```


### Jouer avec les touches du clavier

Lorsqu'on appuie sur la fléche gauche du clavier le sucre réduit et inversement pour la flèche droite. 

* Fonction JS dans le fichier script.js
```javascript
function sugarFunction(event) {
    var key = event.keyCode; //la variable Key est l'évènement d'une touche
    if (key == 37) {
        let nbActuelSucreForm = parseInt($('.choixSucre').val());
        removeSugar();
        $(this).attr('src', 'image_machine/Vue1-assets/Bouton_moins_etat2.png');
        if (nbActuelSucreForm > 0) {
            $('.choixSucre').val(nbActuelSucreForm - 1);
            $('#bonhommeSucre').attr('src','image_machine/Vue1-assets/sugar'+(nbActuelSucreForm-1)+'.png');
        };
    } else if (key == 39) {
        let nbActuelSucreForm = parseInt($('.choixSucre').val()); //je récupère la valeur du nombre de sucre sélectionné
        addSugar();
        $(this).attr('src', 'image_machine/Vue1-assets/Bouton_plus_etat2.png');
        if (nbActuelSucreForm < valeurMaxStock) {
            $('.choixSucre').val(nbActuelSucreForm + 1);
            $('#bonhommeSucre').attr('src','image_machine/Vue1-assets/sugar'+(nbActuelSucreForm+1)+'.png');
        };
    }
};
```

* Dans la vue blade, il faut ajouter l'évènement qui est "lorsqu'on appuie sur la touche" dans la balise Body
```php
<body onkeydown="sugarFunction(event);">
// 'onkeydown' : lorsqu'on appuie sur la touche
```


