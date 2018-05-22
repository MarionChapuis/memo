# PHP AVANCE 

## Projet t-shirt 

Création d'une interface pour la personnalisation de t-shirts.

### Créer le projet 

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
* 


#### Utilisation 

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
        //Chemin des images
        $cheminLogo = public_path("img/logos/" . $logo->id . ".png");
        $cheminTshirt = public_path("img/tshirts/" . $tshirt->id . ".png");

        //instance de ImageManager
        $manager = new ImageManager();

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

## Helpers Laravel 

| Helper | Action | Exemple
|:-------:| -------| -------
| public_path() | Permet d'accèder directement au répertoire public | public_path("img/logos/photo.png");
| storage_path() | Permet d'accèder directement au répertoire storage | storage_path("img/logos/photo.png");

#### Créer un input pour télécharger une image 

Pour télécharger une image depuis le disque interne : 
```html
<input type="file">
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
return [
    ....
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

