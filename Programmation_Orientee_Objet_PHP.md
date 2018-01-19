# Programmation orientée objet

## Définitions  

### Définition d'une classe

Une classe est une **entité regroupant des variables et des fonctions**. Chacune de ces fonctions aura accès aux variables de cette entité.

Une classe est un **regroupement logique de variables et fonctions que tout objet issu de cette classe possédera**.

La classe contient le plan de fabrication d'un objet et on peut s'en servir autant qu'on veut afin d'obtenir une infinité d'objets.


### Définition d'une instance 

Une instance est le résultat d'une instanciation. Instancier c'est se servir d'une classe pour créer un objet.

Une **instance est un objet**.


### Définitions d'attributs et méthodes

Les objets contiennent des attributs et des méthodes. 

**Attribut = Variable** 

**Méthode = Fonction**


### Visibilité d'un attribut ou d'une méthode 

La visibilité d'un attribut ou d'une méthode indique à partir d'où on peut y avoir accès.

* Public = accessible partout 
* Protected = accessible par la classe et ses enfants uniquement 
* Private = accessible par la classe uniquement

## Syntaxe de base 


### Créer une classe 

```php
<?php
	class NomClasse
	{
		//Déclaration des attributs et méthodes
	}
```


### Créer des attributs

```php
<?php 
	class Personnage
	{
		private $_force = 50 ;        // Force du personnage
		private $_localisation; 	  // Sa localisation
  		private $_experience = 1 ;    // Son expérience
  		private $_degats = 0 ;        // Ses dégâts
	} 
```

*La notation PEAR indique que chaque nom d'élément privé (attribut ou méthode) doit être précédé d'un "_".*

*Le nom des classes commence par une majuscule.*

### Créer des méthodes 

```php
<?php 
	class Personnage
	{
		public function deplacer()  // Méthode qui déplacera le personnage
		{

		}
	}
```


### Créer un objet 

```php
<?php
	$variable = new NomClasse() ; 
	$perso = new Personnage() ;
```

$perso est donc un objet de type Personnage, nous avons créée une instance de la classe Personnage. 


### Appeler les méthodes de l'objet

Pour appeler une méthode d'un objet, on utilise l'opérateur "->" : **objet -> méthode();** .

```php
<?php 
	class Personnage {
		public function parler()
		{
			echo "Bonjour";
		}
	}

	$perso = new Personnage() ; 
	$perso->parler(); //appeler la méthode parler() sur l'objet $perso
```


### Accéder à un élément depuis la classe

Lorsqu'un **attribut est Public** on peut y accèder de la manière suivante :

```php
<?php 
	class Personnage {
		public $name = "Marion";
	}

	$perso = new Personnage ; 
	$perso->$name; // on accède directement à la variable
```

Cette syntaxe retournera une erreur lorsque l'attribut est **Private**.

Il faut donc **utiliser une méthode dans la classe pour accèder à l'attribut**. 


#### Comment accèder à l'attribut dans notre méthode ? $this

```php
<?php
	class Personnage
	{
	  private $_experience = 50;

	  public function afficherExperience()
	  {
	    echo $this->_experience;
	  }

	  public function gagnerExperience()
	  {
	    // On ajoute 1 à notre attribut $_experience.
	    $this->_experience = $this->_experience + 1;
	  }
	}
	    
	$perso = new Personnage;
	$perso->gagnerExperience();   // On gagne de l'expérience
	$perso->afficherExperience(); // On affiche la nouvelle valeur de l'attribut
```

**$this permet à la méthode de connaître l'attribut** (qu'il soit public ou private). 
Il s'agit là, de la notion de portée. 

**A noter, avec $this, lorsqu'on note l'attribut il faut supprimer le "$"**.


### Implémenter d'autres méthodes 

**Interaction entre les objets** : par exemple, nous voulons une méthode frapper() qui inflige des dégâts à un autre joueur (un autre objet).

```php
<?php
class Personnage
{
  private $_degats; // Les dégâts du personnage.
  private $_experience; // L'expérience du personnage.
  private $_force; // La force du personnage (plus elle est grande, plus l'attaque est puissante).
        
  public function frapper($persoAFrapper)
  {
    $persoAFrapper->_degats += $this->_force;
  }
        
  public function gagnerExperience()
  {
    // On ajoute 1 à notre attribut $_experience.
    $this->_experience = $this->_experience + 1;
  }
}
```

Descriptions :
* "$personAFrapper->degats" : on veut assigner une nouvelle valeur à l'attribut "$degats" du personnage à frapper
* "+= $this->force" : on donne la valeur que l'on souhaite assigner, on ajouter au dégat du perso2 la force du perso1 ($this).



### Exiger des objets en paramètre 

Il est possible dans une **méthode d'exiger en paramètre un objet** : nomfonction(nomClasse $paramètre) 

Par exemple, nous voulons que la fonction "frapper" est en paramètre uniquement une instance de Personnage. C'est à dire un objet de la classe Personnage.

```php
<?php
class Personnage
{
  // …

  public function frapper(Personnage $persoAFrapper)
  {
    // …
  }
}
```



## Accesseurs et mutateurs 

Lorsqu'un attribut est privé seule la classe peut le lire et le modifier. 


### Accéder à un attribut : l'accesseur - GETTER

Pour accèder à un attribut, nous utilisation des méthodes donc le rôle sera de nous donner l'attribut demander : ce sont des **accesseurs *(ou getters)***. 

Par convention, l'accesseur porte le même nom que l'attribut qu'il retourne.

```php
<?php 
	class Personnage
	{
		// la méthode force() : elle se charge de renvoyer le contenu de l'attribut $_force

	  public function force()
	  {
	    return $this->_force;
	  }
	}
```


### Modifier la valeur d'un attribut : les mutateurs - SETTER

Lorsqu'on souhaite **modifier un attribut, la classe doit impérativement contrôler la valeur** afin d'assurer son intégrité.

Les méthodes permettant de modifier la valeur d'un attribut se nommes : **mutateurs**.

Leur forme : setNomDeLAttribut()

```php
<?php
	class Personnage 
	{
		public function setForce($force)
		{
			if (!is_int($force)) // S'il ne s'agit pas d'un nombre entier.
		    {
		      trigger_error('La force d\'un personnage doit être un nombre entier', E_USER_WARNING);
		      return;
		    }
    
		    if ($force > 100) // On vérifie bien qu'on ne souhaite pas assigner une valeur supérieure à 100.
		    {
		      trigger_error('La force d\'un personnage ne peut dépasser 100', E_USER_WARNING);
		      return;
		    }
		    
		    $this->_force = $force;
		}
	}
```


## Constructeur

Le **constructeur** permet d'**initialiser les attributs d'un objet dès sa création**.

Le constructeur est exécuté dès la création de l'objet.

```php
<?php
	public function __contruct($paramètre)
	{
		//code
	}
```


*Exemple :*
```php
<?php
	class Personnage
	{
		private $_force;
		private $_localisation;
		private $_experience;
		private $_degats;

		public function __construct($force, $degats) // Constructeur demandant 2 paramètres
		{
			echo 'Voici le constructeur !'; // Message s'affichant une fois que tout objet est créé.
			$this->setForce($force); // Initialisation de la force.
			$this->setDegats($degats); // Initialisation des dégâts.
			$this->_experience = 1; // Initialisation de l'expérience à 1.
	  	}
	}
```

*Création de l'objet :*
```php
<?php
	$perso1 = new Personnage(60, 0); //60 de force, 0 de dégât
```

**Ne jamais mettre une méthode construct avec la visibilité private**



## L'opérateur de résolution de portée 

L'opérateur de résolution de portée '**::**', appelé "double deux points" est utilisé pour **appeler des éléments appartement à telle classe et non à tel objet**.

* **Eléments statiques** : attributs et méthodes appartenant à la classe

* **Constantes de classe** : attribut dont la valeur est constante


### Constantes de classe 

A noter : une **constante de prend pas de "$"** devant son nom et est **en majuscule**

**Pour accèder à une constante : NomClasse::Nom_Constante**

*Exemple :*

```php
<?php
	class Personnage
	{
	  private $_force;
	  
	  // Déclarations des constantes en rapport avec la force.

	  const FORCE_PETITE = 20;
	  const FORCE_MOYENNE = 50;
	  const FORCE_GRANDE = 80;

	  public function __construct($forceInitiale)
	  {
	    // N'oubliez pas qu'il faut assigner la valeur d'un attribut uniquement depuis son setter !
	    $this->setForce($forceInitiale);
	  }

	  public function setForce($force)
	  {
	    // On vérifie qu'on nous donne bien soit une « FORCE_PETITE », soit une « FORCE_MOYENNE », soit une « FORCE_GRANDE »

	    if (in_array($force, [self::FORCE_PETITE, self::FORCE_MOYENNE, self::FORCE_GRANDE]))
	    {
	      $this->_force = $force;
	    }
	  }
	}

	//création du personnage avec une force moyenne
	$perso = new Personnage(Personnage::FORCE_MOYENNE);
```


**self::FORCE_PETITE** : fait appel à la classe elle-même 



### Les attributs et méthodes statiques 

#### Les méthodes statiques 

Les méthodes statiques sont faites pour **agir sur une classe et non sur un objet**. La méthode ne doit donc pas utiliser $this.

* **Syntaxe de création : public static function nomFonction() {}**
* **Syntaxe d'appel : Classe::nomFonction();**

*Exemple :*
```php 
<?php 
	public static function parler()
  	{
    	echo 'Je vais tous vous tuer !';
  	}
```



#### Les attributs statiques 

Le principe est le même, c'est-à-dire qu'un attribut statique **appartient à la classe et non à un objet**. Ainsi, **tous les objets auront accès à cet attribut et cet attribut aura la même valeur pour tous les objets**.




* **Syntaxe de création : private static $\_nomAttribut ;**
* **Syntaxe d'appel dans une méthode : self::$\_nomAttribut ;**



## Manipulation de données stockées  

* Etape 1 : créer une classe avec comme attributs les champs de la BDD 

* Etape 2 : créer les getter et les setter pour ces attributs 


### L'hydratation 



## L'héritage

Lorsque la classe B (l'enfant) hérite de la classe A (le parent), la classe B **hérite de l'ensemble des attributs et méthodes publiques** de la classe A.

Les attributs étant en général privés, la classe B héritera uniquement des méthodes publiques.

Il faut procéder à un héritage quand on peut dire que B est un A (ex : un chien est un aniaml).


### Procéder à un héritage : extends

``` php
<?php 
	class Personnage
	{
	
	}

	class Magicien extends Personnage    // Magicien hérité des attributs et méthodes publiques de Personnage
	{

	}
```


Chaque classe peut créer des attributs et méthodes qui lui seront propres, en plus des attributs et méthodes hérités. 

*Si vous essayez d'accéder à un attribut privé de la classe parente, aucune erreur fatale ne s'affichera, seulement une notice si vous les avez activées disant que l'attribut n'existe pas.*


### Redéfinir les méthodes : parent::

Il est **possible de réécrire les méthodes** de la classe Parent dans la classe Enfant.

Il suffit d'appeler la méthode parente avec : **parent::méthodeAAppeler();** 

*Exemple*
```php
<?php 
	public function gagnerExperience()
	{
		parent::gagnerExpercience();  //On appelle la méthode gagnerExperience de la classe parente
		if ($this->_magie < 100) {
			// ...
		}
	}
```

/!\ : On ne peut redéfinir en PRIVATE une méthode qui était PUBLIC


## Imposer des contraintes

### Abstraction des classes : abstract class NomClasse

* Permet d'empêcher qu'une classe soit instancier
* Utile si on veut faire de cette classe un modèle sans pour autant l'instancier
* Cette classe aura donc uniquement des enfants 

*Exemple :*

```php
<?php 
	abstract class Personnage // Notre classe Personnage est abstraite
	{ /*...*/ }

	class Magicien extends Personnage // Création d'une classe Magicien héritant de la classe Personnage
	{ /*...*/}

	$magicien = new Magicien(); // Tout va bien, la classe Magicien n'est pas abstraite.
	$perso = new Personnage(); // Erreur fatale car on instancie une classe abstraite.

```


### Abstraction d'une méthode: abstract public function nomFonction

* Pour qu'une méthode soit abstraite il faut que la classe elle même soit abstraite




## Classes finales : final class NomClass

* Il ne pourra **pas avoir de classe héritant** de la classe Final


## Méthodes finales : final public function nomFonction

* Les classes enfants ne pourront **pas redéfinir la méthode**


## Accèder aux attributs et méthodes sans instancier : public STATIC méthode/attribut

* Permet d'accèder à un attribut ou une méthode sans instancier 

*Exemple :*
```php
<?php
    class King {
        public static function proclaim() {
            echo "A kingly proclamation!";
        }
    }
    
    King::proClaim(); // Fait appel à la méthode proClaim()
```



## Le mot clé : SELF 









# Ressources :

[Mémo POO](http://www.logicbig.com/tutorials/misc/php/php-oop-cheat-sheet/)