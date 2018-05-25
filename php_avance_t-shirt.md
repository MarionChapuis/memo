# PHP AVANCE - PROJET TSHIRT

Objectif : créer une interface pour la personnalisation de t-shirts.


## Helpers Laravel 

| Helper | Action | Exemple
|:-------:| -------| -------
| public_path() | Permet d'accèder directement au répertoire public | public_path("img/logos/photo.png");
| storage_path() | Permet d'accèder directement au répertoire storage | storage_path("img/logos/photo.png");


## Créer le projet 


* Vérifier que Composer est installé 
```bash
composer -v
```
* Installer Laravel 
```bash
composer global require "laravel/installer"
``` 
* Créer le projet Laravel en ligne de commande 
```bash
laravel new NomProjet
```
* Lancer le serveur 
```bash
php artisan serve
```

### Utilisation librairie "Intervention Image"

#### Installation 

* Vérifier la présence de la librairie "GD" (par défaut dans PHP) 
```bash
php -i
```
* Chercher les informations sur GD pour vérifier qu'il soit "enabled"
* Installation de la librairie Intervention Image 
```bash
composer require intervention/image
```
* Ajouter dans config/app.php
```php
'providers' => [
	...
	Intervention\Image\ImageServiceProvider::class,	
],
'aliases' => [
	...
	'Image' => Intervention\Image\Facades\Image::class,
]
```
* Dans les controllers, ajouter dans les use 
```php
use Intervention\Image\ImageManager;
```


#### Utilisation 

[Documentation Intervention Images](http://image.intervention.io/getting_started/introduction)

Objectifs :
- Insérer une image dans une autre
- Redimensionner l'image à insérer
- Centrer l'image à insérer 
- Sauvegarder l'image dans un répertoire dans Storage 

A noter : les créations d'images sont stockées dans Storage pour être protégées. Les images non-sensibles sont quant à elles dans "public".

```php 
use Intervention\Image\ImageManager;

public function store(Tshirt $tshirt, Logo $logo)
    {
        //instance de ImageManager
        $manager = new ImageManager();

        //Chemin des images
        $cheminLogo = public_path("img/logos/" . $logo->id . ".png");
        $cheminTshirt = public_path("img/tshirts/" . $tshirt->id . ".png");       

        //Image du tshirt
        $imageTshirt = $manager->make($cheminTshirt);

        //Image du logo redimensionner en respectant les proportions
        $imageLogo = $manager->make($cheminLogo)->resize($tshirt->largeurImpression, $tshirt->hauteurImpression, function ($constraint) {
            $constraint->aspectRatio();
        });

        //Largeur du logo
        $width = $imageLogo->width();
        $height = $imageLogo->height();

        //Calculer le positionnement du logo par rapport à l'angle gauche en fonction de la zone d'impression (tout en centrant)
        $x = intval($tshirt->origineX + (($tshirt->largeurImpression / 2) - ($width / 2)));
        $y = intval($tshirt->origineY + (($tshirt->hauteurImpression / 2) - ($height / 2)));

        //Coller le logo sur le tshirt
        
        $imageTshirt->insert($imageLogo, 'top-left', $x, $y);

        //Sauvegarder l'image
        $cheminSauvegarde = storage_path("creations/" . time() . "_" . $tshirt->id . "_" . $logo->id . ".png");
        $imageTshirt->save($cheminSauvegarde);

        //Retour à l'accueil
        return redirect(route("images.index"));
    }
```

#### Ajouter du texte 

A noter, pour pouvoir définir la taille, il faut obligatoirement choisir une font personnalisée
```php
//Ajouter un texte avec une font personnalisée:
$imageTshirt->text('Copyright Marion', $tshirt->origineX, 1900, function ($font) {
    $font->file('fonts/Bleeding_Cowboys.ttf'); //font personnalisée
    $font->color(array(255, 0, 0, 0.3)); 
    $font->size(80); //en px
});
```
Structure :
```php
$imageTshirt->text('Le texte', positionX, positionY);
```

## Manipulation des fichiers 

#### Supprimer un fichier 

Pour supprimer un fichier il faut utiliser : 
```php
File::delete("cheminDuFichier");

File::delete(public_path("storage/creations/".$logo->id.".png"));
```

#### Créer un input pour télécharger une image 

Pour télécharger une image depuis le disque interne : 
```html
<input type="file">
```

#### Récupérer un fichier uploadé

```php
//Méthode pour récupérer une image externe
public function fileUpload(Request $request)
{
	//Instance de manager
    $manager = new ImageManager();

    //Créer l'image temporaire
    $img = $manager->make($_FILES['photo']['tmp_name']);

    //Récupérer l'extension de l'image
    $extension = explode("/", $img->mime())[1];

    //Enregistrer l'image en BDD
    $data = [
        "nom" => "perso",
        "largeur" => $img->width(),
        "hauteur" => $img->height()
    ];
    $newLogo = Logo::create($data);

    //Sauvegarder l'image dans le répertoire
    $destination = public_path("img/logos/" . $newLogo->id . ".png");
    $img->save($destination);

    //Retour vers la page d'accueil
    return redirect(route("images.index"));
}
```

Récupérer un fichier temporaire : 
```php
$_FILES['champInput']['tmp_name'];

// tmp_name permet de donner un nom temporaire au fichier
```

## Générer PDF 

### Installation librairie

* Installer la librairie 
```bash
composer require barryvdh/laravel-dompdf
```
* Configurer dans config/app.php
```php
<?php
    'providers' => [
    	....
        Barryvdh\DomPDF\ServiceProvider::class,
    ],

    'aliases' => [
        ....
        'PDF' => Barryvdh\DomPDF\Facade::class,
    ]
``` 

### Utiliser la librairie

* Créer la route dans web.php
```php
//------------------GENERER UN PDF------------------------------------------------------------------------
Route::get('generate-pdf','CreationController@generatePDF')->name("telechargerPDF");
```
* Dans le Controller, avoir une méthode pour générer le pdf 
```php
use PDF;
//Donner des infos aux PDF
$data = ['title' => 'Mes créations'];
//Instance du pdf envoyer à la vue avec les infos
$pdf = PDF::loadView('creations.creationsPDF', $data);
//Retourner le téléchargement du pdf
return $pdf->download('creations.pdf');
```
* Créer la vue (dossier creations) creationsPDF.blade.php qui sera notre pdf
```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1>{{ $title }}</h1>
    <p>Mes créations sont ici</p>
</body>
</html>
```


Exemple 
```php
//Générer un PDF
public function generatePDF()
{
	//Donner des infos aux PDF
    $data = [
       'title' => 'Mes créations',
       'creations' => Creation::all()
    ];
    //Instance du pdf retourner à la vue avec les infos
    $pdf = PDF::loadView('creations.creationsPDF', $data);
    //Retourner le téléchargement du pdf
    return $pdf->download('creations.pdf');
    //Afficher le pdf
    //return $pdf->stream('creations.pdf');
}
```


## Dossier Storage

Storage permet de stocker des images qui ne sont pas accessibles par tout le monde comme public.

**Pour faire un lien symbolique avec le dossier "Public"** 
* Ligne de commande :
```bash
php artisan storage:link
```

Il est possible ensuite dans les vues d'accèder aux infos dans storage :
```html
<img src="{{ public_path("storage/creations/28.png") }}" style="max-height : 100px"> 
```



## Queues 

[Doc Laravel](https://laravel.com/docs/5.6/queues)

Les Queues permettent de réaliser des tâches de manière asynchrone, c'est-à-dire réaliser une tâche lourde en fond tout en ne bloquant pas l'application. 

Des priorités entre les tâches peuvent être données. 

Les **Connections** sont les connexions aux drivers permettant de gérer les queues. 

Il est possible d'utiliser autant de Queue Driver que l'on veut.

### Configurer le driver : Database 

* Il est nécessaire de créer une table qui contiendra toutes les tâches.

```bash
php artisan queue:table
```
```bash
php artisan migrate
```

Structure générée pour la migration pour la table 
```php 
public function up()
{
Schema::create('jobs', function (Blueprint $table) {
           $table->bigIncrements('id');
           $table->string('queue')->index();
           $table->longText('payload');
           $table->unsignedTinyInteger('attempts');
           $table->unsignedInteger('reserved_at')->nullable();
           $table->unsignedInteger('available_at');
           $table->unsignedInteger('created_at');
       }
   );
}
```

* Indiquer dans le fichier .env le driver qu'on veut utiliser (normalement QUEUE_DRIVER = sync) 
```bash
QUEUE_DRIVER=database
```

### Créer un Job 

#### Générer une classe Job 

Si le répertoire contenant les jobs n'existe pas dans app/Jobs, il sera automatiquement créé lors de la génération d'une classe job.

* Créer une classe Job nommée ProcessPodcast
```bash 
php artisan make:job ProcessPodcast
```

La classe générée viendra implémenter l'interface Illuminate\Contracts\Queue\ShouldQueue. 

#### Structure de la classe Job 

La méthode "handle" contient ce que doit faire le job.

```php
<?php

namespace App\Jobs;

use App\Podcast;
use App\AudioProcessor;
use Illuminate\Bus\Queueable;
use Illuminate\Queue\SerializesModels;
use Illuminate\Queue\InteractsWithQueue;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Foundation\Bus\Dispatchable;

class ProcessPodcast implements ShouldQueue
{
    use Dispatchable, InteractsWithQueue, Queueable, SerializesModels;

    protected $podcast;

    /**
     * Create a new job instance.
     *
     * @param  Podcast  $podcast
     * @return void
     */
    public function __construct(Podcast $podcast)
    {
        $this->podcast = $podcast;
    }

    /**
     * Execute the job.
     *
     * @param  AudioProcessor  $processor
     * @return void
     */
    public function handle(AudioProcessor $processor)
    {
        // Process uploaded podcast...
    }
}
```

### Dispatcher les Jobs

Une fois la classe Job créée, il faut utiliser "dispatch" dans le controller. 

L'argument passé à "dispatch" est donné par le constructeur de la classe Job (non obligatoire).

```php
<?php

namespace App\Http\Controllers;

use App\Jobs\ProcessPodcast;
use Illuminate\Http\Request;
use App\Http\Controllers\Controller;

class PodcastController extends Controller
{
    /**
     * Store a new podcast.
     *
     * @param  Request  $request
     * @return Response
     */
    public function store(Request $request)
    {
        // Create podcast...

        ProcessPodcast::dispatch($podcast);
    }
}
```

Envoyer un job à la queue par défaut 
```php 
Job::dispatch();
```

Envoyer un job à la queue 'emails'
```php
Job::dispatch()->onQueue('emails');
```

Donner une priorité importante en ligne de commande
```bash 
php artisan queue:work --queue=high,default
```

### Différer les dispatchs

Pour différer l'exécution d'une tâche il est possible d'utiliser la méthode "delay" lorsqu'on effectu le dispatch. 

Par exemple, différer de 10 minutes : 
```php 
<?php

namespace App\Http\Controllers;

use App\Jobs\ProcessPodcast;
use Illuminate\Http\Request;
use App\Http\Controllers\Controller;

class PodcastController extends Controller
{
    /**
     * Store a new podcast.
     *
     * @param  Request  $request
     * @return Response
     */
    public function store(Request $request)
    {
        // Create podcast...

        ProcessPodcast::dispatch($podcast)
                ->delay(now()->addMinutes(10));
    }
}
```

### Enchaîner les jobs 

Il est possible de créer une séquence de tâches à exécuter, les unes après les autres, avec la méthode "withChain".

Attention, si une des tâches ne fonctionne pas, les suivantes ne seront pas exécutées. 

```php
ProcessPodcast::withChain([
    new OptimizePodcast,
    new ReleasePodcast
])->dispatch();
```


### Exemple : Générer un pdf avec une Queue

* Générer le Job : classe ProcessPDF en ligne de commande 
```bash
php artisan make:job ProcessPDF
```
* Implémenter la méthode handle() en mettant ce qui va être effectué
```php
<?php

namespace App\Jobs;



use Illuminate\Bus\Queueable;
use Illuminate\Queue\SerializesModels;
use Illuminate\Queue\InteractsWithQueue;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Foundation\Bus\Dispatchable;
use App\Creation;
use PDF;

class ProcessPDF implements ShouldQueue
{
    use Dispatchable, InteractsWithQueue, Queueable, SerializesModels;


    /**
     * Create a new job instance.
     *
     * @return void
     */
    public function __construct()
    {

    }

    /**
     * Execute the job.
     *
     * @return void
     */
    public function handle()
    {
        //Donner des infos aux PDF
        $data = [
            'title' => 'Mes créations',
            'creations' => Creation::all()
        ];

        //Instance du pdf retourner à la vue avec les infos
        $pdf = PDF::loadView('creations.creationsPDF', $data);
        //Sauvegarder le pdf
        $pdf->save('creations.pdf');
    }
}
```
* Dans le Controller, effectuer le dispatch 
```php
//Générer un PDF
public function generatePDF()
{
    //Générer le pdf via une Queue
    ProcessPDF::dispatch();
    //Rester sur la même page
    return back();
}
```

* Dans un Bash, lancer en ligne de commande, l'écoute des jobs 
```bash
php artisan queue:work
```
* Laisser ouvert le bash avec la commande et lorsqu'un Job sera demandé, il va être stocké dans la BDD (table jobs) puis exécuté dès que possible grâce à "php artisan queue:work"




## Envoyer un email

[Laravel Doc](https://laravel.com/docs/5.6/mail)

### Installer Guzzle 

Il est obligatoire d'installer, pour toutes les API, Guzzle en ligne de commande : 
```bash
composer require guzzlehttp/guzzle
```

### Choisir un Driver : MAILGUN

Par exemple, utiliser Mailgun (créer un compte sur Mailgun et récupérer son domaine et sa clé). 

* Dans config/mail.php, remplacer "smtp" par mailgun dans le driver :
```php
'driver' => env('MAIL_DRIVER', 'mailgun'),
```
* Il est également possible de déclarer un FROM global si tous les emails sont envoyés depuis le même FROM, dans le fichier config/mail.php
```php
    'from' => [
        'address' => env('MAIL_FROM_ADDRESS', 'postmaster@sandb****************3ab6d.mailgun.org'),
        'name' => env('MAIL_FROM_NAME', 'M(arion)&S(ergio)'),
    ],
```
* Dans config/services, il faut conserver la configuration suivante car c'est dans le .env que cette config ira chercher le "MAILGUN_DOMAIN" & "MAILGUN_SECRET" :
```php
    'mailgun' => [
        'domain' => env('MAILGUN_DOMAIN'),
        'secret' => env('MAILGUN_SECRET'),
    ],
```
* Modifier dans le fichier .env les informations suivantes
```bash
#Parametrer l'envoi d'email
MAIL_DRIVER=mailgun
MAILGUN_DOMAIN=sandbox1fa*************f3ab6d.mailgun.org
MAILGUN_SECRET=key-1628*********4e6
```
* Télécharger le certificat (premier lien) sur le lien : https://curl.haxx.se/docs/caextract.html 
* Copier le fichier dans : C:\wamp64\bin\php\php7.1.9\extras\ssl 
* Compléter dans le fichier "php.ini" disponible dans (C:\wamp64\bin\php\php7.1.9) en supprimant le point virgule : 
``` 
//lien vers le fichier cacert.pem
curl.cainfo = C:\wamp64\bin\php\php7.1.9\extras\ssl\cacert.pem
```
* Relancer le "php artisan serve" lorsque le .env est modifié


### Générer la classe 

Les classes des emails se stockent dans le répertoire app/Mail (si le répertoire n'existe pas il se créera en même temps que la création de la première classe email).

* En ligne de commande créer la classe 
```bash
php artisan make:mail SendPdf
```

### Paramétrer l'email 

Dans la nouvelle classe créée, il est possible de paramétrer l'email :
```php 
<?php

namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Mail\Mailable;
use Illuminate\Queue\SerializesModels;
use Illuminate\Contracts\Queue\ShouldQueue;

class SendPdf extends Mailable
{
    use Queueable, SerializesModels;

    /**
     * Create a new message instance.
     *
     * @return void
     */
    public function __construct()
    {
        //
    }

    /**
     * Build the message.
     *
     * @return $this
     */
    public function build()
    {
    	//permet de retourner la vue qui sera donc l'email
        return $this->view('creations.mailpdf');
    }
}
```

* Créer la vue de l'email 
```html 
@extends("templates/structure")

@section('contenu')
    <div>Bonjour,</div>
    <div>Vous trouverez ci-joint l'historique de vos créations.</div>
    <div>Bisous</div>
@endsection
```

* Créer la méthode pour envoyer l'email dans le Controller 
```php
//Envoyer un email
public function sendMailPdf()
{
    Mail::to('marion.chapuis@campus-numerique-in-the-alps.com')
        ->cc('sergio.custodio@campus-numerique-in-the-alps.com')
        ->bcc('chapuis.marion@gmail.com')
        ->send(new SendPdf());
    }
```

* Créer une route pour envoyer l'email 
```php
//-----------------------------ENVOYER UN EMAIL----------------------------------------------------------
Route::get('sendmail', 'CreationController@sendMailPdf')->name('sendEmailPdf');
```

*S'il y a une erreur "add your domain ... " il faut ajouter les emails qui peuvent réceptionner nos emails dans mailgun. La personne doit accepter. En effet, pendant les tests c'est le seul moyen.*

### Ajouter une PJ à l'email 

Dans la classe de l'email "SendPdf.php", ajouter dans la méthode *build* la pièce-jointe grâce à "attach" :
```php
public function build()
    {
        return $this->view('creations.mailpdf', $data)
            ->attach(public_path("storage/creations/28.png"));
    }
```

### Ajouter des données personnalisées dans l'email 

Dans la classe de l'email "SendPdf.php", ajouter dans la méthode *build* les données et les retourner avec la vue :
```php
public function build()
    {
        $data = [
            "user" => "Marion"
        ];
        return $this->view('creations.mailpdf', $data)
            ->attach(public_path("storage/creations/28.png"));
    }
```

Méthode dans Laravel (la doc) avec "with":
```php
public function build()
    {
        return $this->view('emails.orders.shipped')
                    ->with([
                        'orderName' => $this->order->name,
                        'orderPrice' => $this->order->price,
                    ]);
    }
```
Et il y aura dans la vue : 
```html
<div>
    Price: {{ $orderPrice }}
</div>
```

### Modifier le sujet de l'email 

Toujours dans la classe de l'email 'Mail/SendPdf.php' ajouter la méthode "subject"
```php
    public function build()
    {
        $data = [
            "user" => "Marion"
        ];
        return $this->view('creations.mailpdf', $data)
            ->subject("Votre t-shirt")
            ->attach(public_path("storage/creations/28.png"));
    }
```

### Envoyer un email avec une Queue 

Dans le Controller, remplacer le 'send' par 'queue' pour l'envoi de l'email et hop le tour est joué :
```php
//Envoyer un email
public function sendMailPdf()
{
        //Envoyer un email tout de suite
		//Mail::to("marion.chapuis@campus-numerique-in-the-alps.com")->send(new SendPdf());

    //Envoyer un email avec une Queue
    Mail::to("marion.chapuis@campus-numerique-in-the-alps.com")->queue(new SendPdf());

    //Rester sur la même page
    return back();
}
```


## Créer une API 

[Doc Laravel](https://laravel.com/docs/5.6/eloquent-resources)

[Super exemple API CRUD](https://www.toptal.com/laravel/restful-laravel-api-tutorial)

* Créer la Classe Ressource :
```bash
php artisan make:resource LogoCollection
```
* Implémenter la classe créée LogoCollection
```php
<?php

namespace App\Http\Resources;

use Illuminate\Http\Resources\Json\ResourceCollection;

class LogoCollection extends ResourceCollection
{
    /**
     * Transform the resource collection into an array.
     *
     * @param  \Illuminate\Http\Request $request
     * @return array
     */
    public function toArray($request)
    {

    	//Permet de retourner l'ensemble de la collection en Json
        return [
            'data' => $this->collection,
        ];
    }
}
```

### API afficher tous les logos : 

* Créer la route dans le fichier Routes\api.php

```php
use App\Logo;
use App\Http\Resources\LogoCollection;

//--------------------------------ROUTES API------------------------------------------------------
Route::get("/logos", function() {
    return new LogoCollection(Logo::all());
});
```

### API afficher un seul logo :

* Créer la route pour afficher un seul logo Routes\api.php
```php
use App\Logo;
use App\Http\Resources\LogoCollection;

//--------------------------------ROUTES API------------------------------------------------------
Route::get("/logos/{logo}", function(Logo $logo) {
    return new LogoCollection(Logo::find($logo));
});
```

### Renommer la collection :

* Dans le fichier AppServiceProvider ajouter : ResourceCollection .... 
```php
public function boot()
{
    Schema::defaultStringLength(191);
    ResourceCollection::withoutWrapping();
}
``` 
* Dans la classe Ressource : modifier le nom de la collection 
```php
public function toArray($request)
{
    return [
       'Logos' => $this->collection,
    ];
}
```

### Ajouter une nouvelle création 

L'exemple ci-dessous permet d'effectuer une requête POST avec des données en JSON pour créer une nouvelle Création composée d'un t-shirt et d'un texte.

* Créer la route avec la méthode POST dans le fichier Routes\api.php
```php
Route::post("/creations", "LogoController@store");
```
* Dans un Controller, implémenter la méthode 'store' :
```php
public function store(Request $request)
    {
        //Récupérer les infos pour créer une nouvelle Creation en BDD
        $creation = Creation::create($request->all());
        //Créer un nouveau champs contenant le lien vers la création
        $creation->infos = public_path("storage/creations/".$creation->id.".png");
        //Récupérer le texte entré
        $creation->texte = $request->input("texte");
        //Instance du tshirt
        $tshirt = Tshirt::find(1);

        //Créer l'image avec le texte
        $manager = new ImageManager();
        $imageTshirt = $manager->make(public_path("img/tshirts/1.png"));
        $imageTshirt->text($creation->texte, $tshirt->origineX, 1000, function ($font) {
            $font->file('fonts/Inkfree.ttf');
            $font->color(array(255, 0, 0, 0.8));
            $font->size(80);
        });

        //Enregistrer dans le répertoire
        $imageTshirt->save($creation->infos);

        //Retourner du json avec une réponse 201
        return response()->json($creation,201);
    }
```
A noter : 
* les champs $creation->infos et texte sont créés temporairement
* $request->all() permet de récupérer toutes les infos JSON entrées

Tester avec POSTMAN : 

* Créer une requête POST sur l'url : http://localhost:8000/api/creations
* Dans Headers indiquer : 
	* key : Content-type
	* value : application/json
* Dans Body, sélectionner "raw" et entrer les données JSON :
```json
{
    "tshirt_id" : 1,
    "logo_id" : 0,
    "user_id" : 1,
    "texte" : "Alors, tu valides ????"
}
```
* La réponse sera au format json également en ajoutant le lien vers l'image créée
```json
{
    "tshirt_id": 1,
    "logo_id": 0,
    "user_id": 1,
    "updated_at": "2018-05-25 09:37:40",
    "created_at": "2018-05-25 09:37:40",
    "id": 55,
    "infos": "C:\\wamp64\\www\\tShirt\\public\\storage/creations/55.png",
    "texte": "Alors, tu valides ????"
}
```
