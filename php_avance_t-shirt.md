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



