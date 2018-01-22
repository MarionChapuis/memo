# Programmation orientée objet

## Définitions

* **Classe** = Entité regroupant des attributs (variables) et des méthodes (fonctions)
* **Instance** = objet créée à partir d'une classe 
* **Attribut** = Variable 
* **Méthode** = Fonction


## Visibilité d'un attribut ou d'une méthode 

La visibilité d'un attribut ou d'une méthode indique à partir d'où on peut y avoir accès.

* **Public** = accessible partout
* **Protected** = accessible par la classe et ses enfants uniquement 
* **Private** = accessible par la classe uniquement

*Exemple :*
```php
<?php 
	class Personne 
	{
		public $nom ;
		protected $prenom ;
		private $_age ; 
	}

	$toto = new Personne() ; 

	// Fonctionne car l'attribut est public
	$toto->nom ;
```


## Syntaxes

La notation PEAR indique les conventions suviantes : 
* Attribut ou méthode **privé** précédé d'un "\_" : $\_attribut
* Le **nom** d'une **classe** commence par une **majuscule**

### Créer une classe avec des attributs et des méthodes

```php
<?php
	class NomClasse
	{
		private $_attribut = 5;
		protected $attribut = "toto";
		public $attribut = "bonjour";	

		public function nomFonction(paramètre)  // Méthode
		{
			//...
		}
	}
```


### Créer une instance

```php
<?php
	$variable = new NomClasse() ; 
```


### Appeler une méthode de l'objet

* Utiliser l'opérateur "->" : **objet -> méthode();** 
```php
<?php
	$objet->methode() ; 
```



## Getter : afficher un attribut

* Getter : méthode dans la classe permettant d'afficher un attribut (porte le **nom de l'attribut**)

```php
<?php 
	class Personne 
	{
		public function nomAttribut()
		{
			return $this->nom ;
		}
	}
	$toto = new Personne() ; 
	echo $toto->nom() ; //affiche le nom
```


## Setter : modifier un attribut

* Setter : permet de gérer la modification un attribut (**porte le nom : setAttribut**)

```php
<?php 
	class Personne 
	{
		public function setNom($name)
		{
			$this->nom = $name ;
		}
	}
	$toto = new Personne() ; 
	$toto->setNom('Dupont') ; // Modifie l'attribut "nom" de l'objet $toto par "Dupont"
```


## Constructeur 

* Permet de structurer la création d'une instance, en par exemple pré-remplissant les champs souhaités
* Lors d'une instanciation, le constructeur est automatiquement appelé 

```php
<?php 
	class Personne 
	{
		public function __construct($name)
		{
			$this->nom = $name ;
		}
	}
	$toto = new Personne("Dupont") ; Crée l'instance $toto avec pour attribut Nom = "Dupont"
```


## $this : accéder à un attribut dans une méthode

* Permet à la méthode de connaître l'attribut qui est dans sa classe (peu importe sa visibilité) 

```php
<?php 
	class NomClasse 
	{
		protected $attribut = "chainedecaractères" ;

		public function __construct($parametre)
		{
			$this->attribut = $parametre ;
		}
	}

	$instance = new NomClasse("parametre") ; // Crée l'instance avec comme valeur de $attribut = $parametre
```



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



# Ressources :

[Mémo POO](http://www.logicbig.com/tutorials/misc/php/php-oop-cheat-sheet/)



# POO : point commun 


## Static 

* Permet d'appeler les méthodes et attributs Static sans les instancier
* Simplifie la vie : exécute la méthode sans créer l'objet

```php
<?php 
	class Boisson 
	{
		public static function find($id)
		{
			//en SQL SELECT FROM Boissons WHERE id = $id;
			return ...;
		}
	}
	
	Boisson::find(12) ; // Affiche l'objet boisson dont l'id est 12 sans même créer une instance
```


## Accèder à des attributs ou méthodes 

$instance->attribut(qui est également une instance)->attribut


## Héritage : class ClasseEnfant extends ClasseParent

* Récupère tous les attributs et méthodes (sauf les privés)


## self:: 

* Dans les méthodes normales on utilise $this

* Dans les méthodes statics on utilise self::

```php
<?php 
	class Math 
	{
		const q = 1 ; //si cet attribut n'était pas static, la fonction suivante ne fonctionnerait pas

		public static function sommeQ ($a, $b)
		{
			return $a + $b + self::q
		}

		Math::sommeQ(1 , 12); //Affichera 14
	}
```

*self:: est peu utilisé*

