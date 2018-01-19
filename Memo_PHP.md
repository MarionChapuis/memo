# Mémo PHP


## Syntaxes de base 


Balises pour mettre du code php :
```php
<?php tapez le code ici; ?>
```


**.** : opérateur de **concaténation** 
```php
<?php echo "Bonjour" .$maVariable. " !"; ?>
```


**$** : **définir une variable** - attention sensible à la casse 
```php
<?php $maVariable = "Marion"; ?>
```


**;** : toutes les déclarations doivent se terminer par un ;
```php
<?php function maFonction() {
		echo "Bonjour" ;
	} ?>
```


**//** : ajouter un **commentaire** dans du code php
```php
<?php mafonction() //Appeler ma fonction ?>
```



## Les comparaisons



| Opérateur | Signification |         
| :-------: |:-------------:|
| >         | Est supérieur à
| <         | Est inférieur à
| <=        | Est inférieur ou égal à 
| >=        | Est supérieur ou égal à 
| ==        | Est égal à
| !=         | Est différent de (est non égal à)


## Les conditions


### if ... else

```php
<?php
	if ($nbArticles > 8) {
		echo « Réduction de 10 %» ;
	}	
	else if ($nbArticles > 4) {
		echo « Réduction de 5 %» ;
	}
	else {
		echo « Réduction de 1 %» ;
	}	 
?>
```


### switch

```php
<?php
	switch($variable) {
		case « Pomme » :
			echo « C’est une pomme» ;
		break ;
		case « Poire » :
		case « Peche » :
			echo « C’est une pêche ou une poire » ;
		break ;
		default :
			echo « C’est une pomme» ;
	}	 
?>
```


### switch ... endswitch

```php
<?php
	switch($variable) :
		case « Pomme »
			echo « C’est une pomme» ;
		break ;
		case « Poire » :
		case « Peche » :
			echo « C’est une pêche ou une poire » ;
		break ;
		default :
			echo « C’est une pomme» ;
	endswitch ;	 
?>
```



## Les tableaux

**Déclarer un tableau**

```php
<?php
	$tableau = array("Vert" , "Jaune") ;

	//Depuis la version 5.4, il existe également la syntaxe 

	$tableau = ["Vert" , "Jaune"] ;
?>
```


**Accèder** aux éléments

```php
<?php
	$tableau[0] ; //affichera le premier élément du tableau
?>
```


**Modifier** un élément

```php
<?php
	$tableau[0] = "Rose" ; 
?>
```


**Supprimer** un élément d'un tableau

```php
<?php
	unset($tableau[1]) ; 
?>
```



## Les tableaux associatifs : une clé associée à une valeur


**Déclarer** un tableau associatif 

```php
<?php
	$recettes = array ("cafeLong" => array(
										"Cafe" => 2,
										"Eau" => 3),
						"latte" => array(
										"Cafe" => 1,
										"Eau" => 2,
										"Lait" => 4)
				) ; 
?>
```

***Avec la nouvelle syntaxe***

```php
<?php
	$recettes = ["cafeLong" => [
								"Cafe" => 2,
								"Eau" => 3
								],
				"latte" => [										"Cafe" => 1,
							"Eau" => 2,
							"Lait" => 4
							]
				] ; 
?>
```


**Afficher l'ensemble des éléments d'un tableau associatif : boucle FOREACH**

```php
<?php
	foreach ($recette as $key => $unElement) {
		echo $key . "*" .$unElement ;
	}
	//affichera Café * 2 Eau * 3 ...
?>
```



## Les boucles 

**for** : jusqu'à

```php
<?php
	for ($i = 0 ; $i < 10 ; $++) {
		echo $i ;
	}
?>
```


**foreach** : pour chaque

```php
<?php
	foreach ($mesNombres as $unNombre) {
		echo $unNombre ;
	}
?>
```


**while** : tant que

```php
<?php
	while ($nombre < 10) {
		echo $nombre ;
		$nombre ++; //nombre s'incrémente de 1 à chaque tour de boucle
	}
?>
```


**while ... endwhile** : tant que

```php
<?php
	while ($nombre < 10) :
		echo $nombre ;
		$nombre++; //nombre s'incrémente de 1 à chaque tour de boucle
	endwhile ;
?>
```


**do..while** : Exécuter le code au moins une fois

La condition est vérifiée seulement après chaque itération, le code sera donc exécuté au moins une fois 

```php
<?php
	$nb = 0 ;
	do {
		$nb++ ; 
		echo $nb ;
	} while ($nb < 10) ;
?>
```



## Les fonction pour les chaînes de caractères 

**round (chiffre, ndDécimal)** : arrondir les nombres décimaux

**M_PI** : valeur de PI

**rand (min, max)** : retour un nombre aléatoire entre le min et le max

**strlen ("Marion")** : calculer le nombre de caractères d'une chaîne de caractères

**substr ($laChaine , position du 1er caractère , nb caractères à extraire)** : extraire une partir d'une chaîne de caractères

**strtotupper ($chaine)** : transformer en majuscule la chaîne de caractères

**strtolower ($chaine)** : transformer en minuscule la chaîne de caractères

**strpos ($chaine , élément recherché)** : recherche un extrait dans une chaîne de caractères puis retour comme résultat la position du premier caractère de l'extrait trouvé ou faux si ce n'est pas trouvé



## Les fonctions de tableaux 

**array_push ($tableau , "élément à ajouter")** : ajouter un élément à la fin du tableau

**count ($tableau)** : retour le nombre d'élément d'un tableau

**sort ($tableau)** : trie les éléments d'un tableau et retour vrai ou faux(en cas d'échec)

**tsort ($tableau)** : trie les éléments d'un tableau dans l'ordre inverse et retour vrai ou faux(en cas d'échec)

**join ("Séparateur" , $tableau)** : crée une chaîne de caractères avec les éléments d'un tableau avec la possibilité de choix le type de séparateur entre les éléments



## Syntaxe d'une fonction 

*A noter, le nom des fonction est insensible à la casse*

```php
<?php
	function nomFonction (paramètre) {
		echo "instructions" ; // affiche "instructions"
		return "instructions" ; // n'affichera pas, mais le résultat de la fonction sera "instructions" 
	}
?>
```

**Bonne pratique** : 
Favoriser un maximum **return** dans une fonction puis afficher le résultat de cette fonction dans le HTML avec un **echo**.

*Exemple :*

```php
<?php
	function preparer ($tableau) {
		$liste = "";
		foreach ($tableau as $key => $unElement) {
			$liste = $liste . "<li>" .$key. " * " .$unElement. "</li>" ; 
		} ;
		return $liste ; 
	}
?>
```



## Les scopes

Une fonction est une véritable boîte noire !

Les variables dans une fonctions ne sont pas connues dans le reste du programme.

Les variables dans le programme ne sont pas connues dans une fonction.

**Permettre à une fonction de connaître une variable globale**

```php
<?php
	$recettes = ["Café" , "Sucre"] ; 
	function $mafonction () {
		global $recettes ; 
		echo $recettes ; //affichera bien le tableau $recettes
	}
?>
```



## Fonctions PHP 

Pour **modifier une variable globale avec une fonction**, il faut ajouter un "&" devant le paramètre lorsque la fonction est créée.

*Exemple*

```php
<?php
	function majstock ($tableauIng , &tableauStock) {
		foreach ($tableauStock as $keyStock => $valueStock) {
			echo $tableauStock[$keyStock] = $tableauStock[$keyStock] - 3;
		}
	}
?>
```



## Debuguer 

**var_dump ($tableau ou $variable)** : Affiche la structure et les informations sur le tableau ou la valeur d'une variable

**print_r ($tableau ou $variable)** : Affiche les informations sur le tableau ou la variable mais moins précis que *var_dump*

Consulter le fichier **PHP error log** : journal des erreurs rencontrées sur le programme



## Fonctions 


|Nom de la fonction | Rôle de la fonction | Exemple
:------------------:|:-------------------:| :--------:
| date ("l j F Y")  | Retourne la date et l'heure locale avec la forme demandée dans les paramètres| Ressources  [Site documentation PHP](http://php.net/manual/fr/function.date.php)



# Ressources 

[Mémo PHP](http://www.logicbig.com/tutorials/misc/php/php-cheat-sheet/)