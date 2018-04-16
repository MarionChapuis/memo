# Java

[Super mémo Java](http://thierry-leriche-dessirier.developpez.com/tutoriels/java/mots-cles-java/#LIV-B-9)

## Définition & Installation

JAVA est un langage compilé et typé.

JDK : Java Development Kit (librairie JAVA avec notamment 'javac' le compilateur)

JRE : Java Environment Execution (permet d'éxécuter sur l'ordinateur)

Le code est exécuté par une machine virtuelle grâce au JRE et JDK.

## Mots clés 

| Mot clé | Définition  
|:-----:|---------
| Classe |Entité regroupant des attributs (variables) et des méthodes (fonctions)
| Instance | objet créée à partir d'une classe 
| Attribut | Variable 
| Méthode | Fonction
| Getter | méthode dans la classe permettant de retourner un attribut
| Setter | méthode dans la classe permettant de gérer la modification d'un attribut
| Constructeur | Permet de structurer la création d'une instance (Lors d'une instanciation, le constructeur est automatiquement appelé)
| Héritage (extends) | Lorsque la classe B (l'enfant) hérite de la classe A (le parent), la classe B hérite de l'ensemble des attributs et méthodes publiques de la classe A (on peut dire que B est un A, - class B extends A)
| Surchargement (overriding) | lorsqu'une méthode d'une classe mère est modifiée dans sa classe fille
| Interface | Contient une ou des méthodes qui peuvent être utilisées par plusieurs classes différentes
| Implementer | Une classe qui implémente une interface définit les méthodes de l'interface
| Abstraite | Une classe abstraite permet de définir des méthodes abstraites qui seront implémentées dans les classes filles. Ainsi les classes filles ont déjà une structure déterminée par la classe mère. Une classe abstraite ne peut être instanciée 
| Concrète | Une classe concrète contient des méthodes concrètes, c'est-à-dire qu'elles sont définies. Ces méthodes peuvent implémenter des méthodes d'une classe abstraite
| Package | Il s'agit d'un dossier qui contient des classes 
| Import | 	Permet d'importer un autre package avec ses classes
| Final | Indique qu'un élément ne peut être ni modifié, ni étendu. Une classe avec le mot clé Final ne peut pas avoir de fille par héritage. Une méthode Final indique que les classes filles ne peuvent pas surcharger la méthode. Appliqué à une variable, il indique que la variable est une constante
| Static | Les méthodes statiques sont faites pour agir sur une classe et non sur un objet. Une méthode statique peut être utilisée sans instancier un objet de la classe
| Void | Indique que la méthode ne retournera pas de valeur (ex : public void maMethode(){System.out.println("je retourne rien");} )



### IDE 

Plusieurs IDE :
* Eclipse [lien](http://www.eclipse.org/)
* IntelliJ IDEA [lien](https://www.jetbrains.com/idea/)
* Netbeans [lien](https://netbeans.org/)
* Visual Studio Code


### Installation Environnement 

* Installer la JDK et JRE (vérifier dans Programmes > Java les versions)
* Paramétrer le PATH : C:\Program Files\Java\jdk1.8.0_161\bin 
* Ajouter une variable "JAVA_HOME" : C:\Program Files\Java\jdk1.8.0_161
* Vérifier en entrant dans un Bash : 
```bash
java -version
javac
```


### Maven 

Maven permet de se faciliter la vie en Java : 
* Gestionnaire de dépendances 
* Récupèrer des librairies sur internet et l'ajouter dans le pom.xml
* mvn install : permet de compiler et installer les dépendances (génère un fichier .jar)

##### Installation Maven 

* Télécharger : [lien](http://maven.apache.org/download.cgi)
* Copier le dossier "apache-maven" (dans le zip) dans : C\Programmes par exemple
* Ajouter dans le PATH : C:\Program Files\apache-maven-3.5.3\bin

Commandes :
* Supprimer les classes et Target
```bash
mvn clean
```
* Compiler 
```bash
mvn compile
```
* Installer les dépendances, à noter cette commande compile d'abord
```bash
mvn install
```
* Nettoyer, compiler et installer les dépendances : **A faire avant de commiter par exemple**
```bash 
mvn clean install
```

## Démarrer un projet Java - Maven

* Créer un répertoire avec l'arborescence "NomRépertoire/src/main/java/hello" en ligne de commande :
```bash
mkdir -p NomRépertoire/src/main/java/hello
```
* Créer le fichier 'pom.xml' avec le minimum suivant, à côté de 'src':
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>fr.campus-numerique-in-the-alps</groupId>
    <artifactId>hello</artifactId> 
    <version>1</version>
    <packaging>jar</packaging>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.1</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <transformers>
                                <transformer
                                        implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                    <mainClass>hello.HelloWorld</mainClass>
                                </transformer>
                            </transformers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <dependencies>
        <dependency>
            <groupId>joda-time</groupId>
            <artifactId>joda-time</artifactId>
            <version>2.9.2</version>
        </dependency>
    </dependencies>
</project>
```
* A noter dans ce fichier :
	* mainClass : fichier principal où on met tout
	* artifactId : version.jar
* Coder en mettant les fichiers java dans 'hello'
* Utiliser Maven :
```bash
mvn compile
mvn install
java -cp target/<artifactId> <mainClass>
//exemple 
java -cp target/hello-1.jar hello.HelloWorld
```
* Créer le Read.me et GIT 

### Dans l'IDE IntelliJ IDEA 

##### Changer la source dans les paramètres pour pouvoir utiliser le bon chemin dans "package NomDossier" (et non main.java.NomDossier) 

* File / Project Structure / Module 
* Clic droit sur le dossier "Java" dans l'arborescence 'src/main/java/NomDossier' 
* Sélectionner "Sources"
* Supprimer dans la partie "Sources Folders" la ligne "src" pour ne conserver que la source que l'on vient de créer

##### Paramètrer la console de débug pour jouer le code :

* En haut à droite il y a une liste déroulante proposant "edit configuration", sélectionner cette partie
* Une fenêtre "Run/Debug Configurations" s'ouvre 
* Cliquer sur le bouton "+" et sélectionner "Application"
* Donner un nom dans le champs "Name"
* Configurer en ajoutant la "Main.class" (NomDossier/ClasseAjouer, ex: hello.HelloWorld)
* Séllectionner "Apply" puis "ok" pour enregistrer les modifs 
* Dans la liste déroulante, il y a à présent notre configuration que l'on peut sélectionner pour exécuter le code


## Exemple HelloWorld 

Consignes : 
* une interface Bonjour avec une méthode sayHello qui renvoie une chaîne de caractères
* une classe abstraite Animal qui implémente l'interface ci-dessus
* deux classes qui étendent d'Animal : Human et Dog
* créer une instance pour chacune des classes concrètes

Créer l'interface Bonjour avec une méthode sayHello qui renvoie une chaîne de caractères
```java
package hello;

public interface Bonjour{
	public String sayHello();
}
```

Une classe abstraite Animal qui implémente l'interface Bonjour
```java
package hello;

public abstract class Animal implements Bonjour {
    public abstract String sayHello();
}

```

2 classes qui étendent d'Animal : Human et Dog
```java
package hello;

public class Human extends Animal {
    public String sayHello(){
        return "Hello";
    }
}
```

Dans le fichier HelloWorld (le mainClass) :
```java
package hello;

public class HelloWorld {
    public static void main(String[] args){
        Animal canardo = new Duck();
        Animal humain = new Human();
        System.out.println("Le canard : "+ canardo.sayHello());
        System.out.println("L'humain : " + humain.sayHello());
    }
}
```


Compiler et installer les dépendances avec Maven :
```bash
mvn install
```

Lancer la classe pour afficher dans le terminal :
```bash
java -cp target/hello-1.jar hello.HelloWorld
```



## Interface 

Contient une ou des méthodes qui peuvent être utilisées par plusieurs classes différentes.

* Créer une interface avec des méthodes :
```java
public interface Bonjour{
  public abstract String sayHello();
  
  public void Combat();

}
```

* Des classes viennent implémenter cette méthode 
```java
public class Humain implements Bonjour {
  
  //Implémenter les méthodes de l'interface
  public String sayHello(){
    return "Bonjour";
  }

  public void Combat(){
    System.out.println("Je lance le combat");
  }

}
```


## Les types de variables 

Une variable est déclaré de la manière suivante et se termine toujours par un ';', ensuite  nt:
```java
<Type de la variable> <Nom de la variable> ;
```

### Les variables de type numérique 

| Type | Contient | Exemple 
|:-----:|---------|---------
| byte | entiers entre -128 et +127 | byte temperature; temperature = 64;
| short | entiers compris entre 32768 et +32767 | short vitesseMax; vitesseMax = 32000;
| int | -2\*109 à 2*109 (2 et 9 zéros derrière) | int temparatureSoleil; temperatureSoleil = 15600000 ; 
| long |  −9×10^18  à 9×10^18, il faut ajouter un L àla fin du nombre | long anneeLumiere; anneeLumiere = 9460700000000000L;
| float | Nombres avec une virgule flottante | float pi; pi = 3.141592653f;
| double | Identique à float mais il contient plus de chiffres derrière la virgule et qu'il ne contient pas de suffixe | double division; division = 0.333333333333333333333333333334d; |


### Les variables stockant des caractères

| Type | Contient | Exemple 
|:-----:|---------|---------
| char | Un caractère stocké entre apostrophes | char caractere ; caractere = 'A' ;
| boolean | true ou false sans guillemmets | boolean question; question = true; 
| String | Chaînes de caractères, il s'agit d'une variable de type 'Objet' | String maVar = "Une chaîne de caractères"

**Attention : String commence par une majuscule ! Et lors de l'initialisation, on utilise des guillemets doubles (« " " »).**

String est un objet, la variable est donc une instance. Le nom d'une classe commence toujours par une majuscule.

Différentes façons de déclarer une variable String : 
```java 
//Première méthode de déclaration
String phrase;
phrase = "Titi et Grosminet";

//Deuxième méthode de déclaration
String str = new String();
str = "Une autre chaîne de caractères";

//Troisième méthode de déclaration
String string = "Une autre chaîne";

//Quatrième méthode de déclaration
String chaine = new String("Et une de plus !");
```

### Compacter les déclarations de variables 

Déclarer et initialiser une variable en une ligne :
```java
int entier = 32;
float pi = 3.1416f;
char carac = 'z';
String mot = new String("Coucou");
```

Déclarer plusieurs variables d'un même type : 
```java
int nbre1 = 2, nbre2 = 3, nbre3 = 0;
```


## Opérateurs 

Le traitement arithmétique s'effectue que sur des variables de même type. 

| Opérateur | Fonction |  
|:-----:|---------|
| + | Additionner et concaténer 
| - | Soustraire 
| * | Multiplier 
| / | Diviser 
| % | Renvoi le reste de la division entière de 2 variables, il s'agit du modulo
| < | Plus petit que
| <= | Plus petit ou égal à 
| > | Plus grand que 
| >= | Plug grand ou égal à 
| == | Egal à 
| != | N'est pas égal
| && | Et 
| \|\| | Ou 
| ! | N'est pas  

**Priorité des opérateurs booléens** 
! : est évalué le 1er
&& : est évalué le 2ème
|| : est évalué le 3ème


Incrémenter 
```java
int nbre1, nbre2, nbre3;    //Déclaration des variables
nbre1 = nbre2 = nbre3 = 0;  //Initialisation

nbre1 = nbre1 + 1;
nbre1 += 1;
nbre1++;
++nbre1;
```

Décrémentation
```java
nbre1 = nbre1 - 1;
nbre1 -= 1;
nbre1--;
--nbre1;
```

Mutiplication - Division 
```java
nbre1 = nbre1 * 2;
nbre1 *= 2;
nbre1 = nbre1 / 2;
nbre1 /= 2;
```

**Afficher le contenu d'une variable dans la console** 
```java
double nbre1 = 10, nbre2 = 3;
int resultat = (int)(nbre1 / nbre2); //retournera un entier : 'int'
System.out.println("Le résultat est = " + resultat);
```

## Conditions 

Syntaxe classique if, else if, else : 
```java
int round = 1;

if (round > 12) {
	System.out.println("The match is over!");
} else if (round > 0) {
	System.out.println("The match is underway!");
} else {
	System.out.println("The boxing match hasn't started yet.");
}	
```

Syntaxe alternative : () ? if : else ;
```java
char maCondition = (monScore > 20) ? 'W' : 'L' ;
```

Syntaxe Switch : 
```java
switch (maCondition) {
	case 1 : /* */ ;
	break;
	case 2 : /* */ ;
	break;
	case 3 : /* */ ;
	break;
	case 4 : /* */ ;
	break;
	default : /* */ ; 
	break;
}
```


## Les boucles FOR 

Pour boucler avec un for:
```java
for (int i = 0 ; i < nomArrayList.size() ; i++){
  System.out.println( nomArrayList.get(i) );
}
```

## Les boucles FOREACH 

Pour "chaque élément dans la liste" :
```java
for (Integer unElement : nomArrayList){
    System.out.println(unElement);
}
```


## Conversion : cast

Convertir des variables se nomme conversion d'ajustement ou **cast** de variable.


Un type 'int' en type 'float'
```java
int i = 123;
float j = (float)i;
```

Un type 'int' en type 'double'
```java
int i = 123;
double j = (double)i;
```

Inversement 
```java
double i = 1.23;
double j = 2.9999999;
int k = (int)i;        //k vaut 1
k = (int)j;            //k vaut 2
```

Caster un résultat : (type du résultat)(calcul) 
```java
double nbre1 = 10, nbre2 = 3;
int resultat = (int)(nbre1 / nbre2);
```


**Exemple : une classe Personnage et 2 classes (Guerrier et Magicien) qui extends de Personnage**

Les guerriers et magiciens sont stockés dans un tableau de type Personnage. 
Nous souhaitons modifier des attributs spécifiques de Guerrier et Magicien.
Mais ce n'est pas possible car ils sont de type Personnage et que cette classe ne connait pas les getters et setters de Guerrier et Magicien.

Solution : changer le type Personnage en un Guerrier ou Magicien
```java
Magicien magicien = (Magicien) monPerso; // monPerso qui était de type Personnage devient de type Magicien
```



## Les entrées claviers 

Utilisation de l'objet **Scanner** pour la lecture des entrées clavier.
* Importer le package 
* Initialiser l'objet Scanner avec l'entrée standard "System.in"
* Il y a une méthode de récupération de données pour chaque type (sauf les char) : nextLine() pour les String, nextInt() pour les int ...

```java
import java.util.Scanner;

public class Main {
  public static void main(String[] args){
    Scanner sc = new Scanner(System.in);
	System.out.println("Veuillez saisir un mot :");
	String str = sc.nextLine();
	System.out.println("Vous avez saisi : " + str);
  }
}
```

Indiquer le type de variable que l'on souhaite récupérer :
```java
Scanner sc = new Scanner(System.in);
int i = sc.nextInt(); //Récupérer un entier 
double d = sc.nextDouble(); // Récupérer un double
long l = sc.nextLong(); 
byte b = sc.nextByte();
```

## Méthodes static 

Pour appeler une méthode static : 
```java
Arme monArme = Arme.maMethodeStatic();
```

## Structurer son projet : package

L'architecture : MonProjet/src/main/java/nomPackagePrincipal 
Exemple : MonProjet/src/main/java/campus

A l'intérieur du package "campus" il est possible de créer d'autres packages contenant des classes (regroupées par utilisation). 

Dans les classes, créer des méthodes "public static" qui pourront être utilisées dans d'autres classes. 
Il faudra alors importer les classes : 
```java
import campus.personnages.*; // * pour tout importer du package "personnages"
```



## Les tableaux 

Un tableau ne peut contenir qu'un seul type de variables et a la structure : <\Type de variables> <\NomTableau>[] = {item, item}; 

#### Tableau simple 
```java
int tableauEntier[] = {0,1,2,3,4,5,6,7,8,9};
double tableauDouble[] = {0.0,1.0,2.0,3.0,4.0,5.0,6.0,7.0,8.0,9.0};
char tableauCaractere[] = {'a','b','c','d','e','f','g'};
String tableauChaine[] = {"chaine1", "chaine2", "chaine3" , "chaine4"};
```

Initialiser un tableau vide est possible mais il faut indiquer le nombre de cases 
```java
int tableau[] = new int [5]; 
```

#### Tableau multidimentionnel 

Il s'agit d'un tableau contenant au minimum 2 tableaux.

```java
int premiersNombres[][] = { {0,2,4,6,8},{1,3,5,7,9} };
```

Pour rechercher un élément : 
```java
premiersNombres[0][1] // correspond dans le premier tableau au 2ème élément : 2
```

## Les classes 

### Les constructeurs 

Si le constructeur n'est pas déclaré dans la classe, il en existe un par défaut qui est vide : public NomConstructeur(){}

**Le nom du constructeur est celui de la Classe**.

```java
public class Ville{   
  //Stocke le nom de notre ville
  String nomVille;
  //Stocke le nom du pays de notre ville
  String nomPays;
  //Stocke le nombre d'habitants de notre ville
  int nbreHabitants;
     
  //Constructeur 
  public Ville(){    
    nomVille = "Inconnu";
    nomPays = "Inconnu";
    nbreHabitants = 0;
  } 
}
```

### Getter et Setter 

Un Getter retourne le nom de la variable : getNomVariable(){}
Un Setter permet de modifier la valeur d'une variable : setNomVariable(){}
```java
public class Ville {
	String nomVille;
          
  //*************   ACCESSEURS - GETTER *************
    
  //Retourne le nom de la ville
  public String getNom()  {  
    return nomVille;
  }

  //*************   MUTATEURS  - SETTER *************

  //Définit le nom de la ville
  public void setNom(String pNom)
  {
    nomVille = pNom;
  }
}
```

### Classes Abstraites & Concrètes

#### Classes Abstraites 

Une classe abstraite permet de définir des méthodes abstraites qui seront implémentées dans les classes filles. 
Ainsi les classes filles ont déjà une structure déterminée par la classe mère. 
Une classe abstraite ne peut être instanciée. 

Les méthodes d'une classes abstraites sont forcément abstraites elles aussi.

```java
public abstract class Animal{
  public abstract String sayHello(); //méthode abstraite retournant une chaîne de caractères
}
```

#### Classes Concrètes 

Une classe concrète contient des méthodes concrètes, c'est-à-dire qu'elles sont définies. 
Ces méthodes peuvent implémenter des méthodes d'une classe abstraite.

```java
public class Felin{
	public String sayHello(){
		return "Miaou"; 
	}
}
```

### Les méthodes 

Lors de la déclaration d'une méthode il faut indiquer 2 choses :
* Sa visibilité : public, private, protected
* Le type de variable qu'elle retourne : String, int ... 

#### Les méthodes retournant un type de variable

```java
public class Felin{
	public String sayHello(){
		return "Miaou"; //la méthode retourne une chaîne de caractères
	}
}
```


#### Void 

Indique que la méthode ne retournera pas de valeur.

```java
public class Felin{
	public void maMethode(){
		System.out.println("je retourne rien");
	}
}
```

#### Void main 

Pour qu'un programme en Java puisse être exécuté, une méthode est absolument indispensable, c’est la méthode main. Elle se déclare toujours de la manière suivante :

```java
package hello;

public class HelloWorld {
    public static void main(String[] args){
        Animal canardo = new Duck();
        Animal humain = new Human();
        System.out.println("Le canard : "+ canardo.sayHello());
        System.out.println("L'humain : " + humain.sayHello());
    }
    public static void autreMethode(){
      //Toutes les autres méthodes doivent être static car "main" est static
    }
}
```

Toutes les autres méthodes doivent être static car "main" qui est le point d'entrée est static.

## Les énumérations 

Une énumération se déclare comme une classe et permet de définir une liste de valeurs possibles. 
Cela permet de créer des types de données personnalisées. 

Syntaxe :
```java
public enum NomEnumeration
{
  valeur1,
  valeur2,
  valeur3
}
```

Exemple : 
Une classe Personnage avec 2 classes qui Extends de Personnage : Guerrier et Magicien. 
Pour pouvoir connaître le type du personnage (Guerrier ou Magicien) il y a une variable "type" dans la classe de personnage.

* Création de l'énumération (créée au-dessus de la classe abstraite Personnage)
```java
public enum PersonnageType
{
    Guerrier,
    Magicien
}
```
* Création d'une variable "type" de type "PersonnageType" dans la classe Personnage 
```java
public abstract class Personnage 
{
    private String nom;
    private String image;
    private String niveauVie;
    private String forceAttaque;
    private PersonnageType type;
}
```
* Création des getter et setter pour "type"
```java
public PersonnageType getType() 
{
  return type;
}

public void setType(PersonnageType ptype) 
{
  type = ptype;
}
```
* Création du constructeur de Personnage en imposant aux classes enfants d'avoir un "type"
```java
public Personnage(PersonnageType type){
  this.type = type;
}
```
* Création du constructeur dans la classe enfant Guerrier qui définit le "type"
```java
public Guerrier()
{
  super(PersonnageType.Guerrier); //super() permet d'appeler le constructeur de la classe mère
}
```
* Vérifier le type d'une instance de Guerrier 
```java
if (personnageToModified.getType() == PersonnageType.Magicien)
{
  //si le type de mon personnage est de type Magicien alors j'exécute le code
}
```

## Instanceof

Vérifier si une variable est une instance d'une classe en retournant un booléen.

Exemple : Vérifier si un personnage est une instance de Magicien 
```java
monPersonnage instanceof Magicien 
```


## Méthode "toString" : afficher les infos d'un objet

La méthode "toString" permettant de convertir en chaîne de caractères les informations d'un objet.

Toutes les classes héritent de la grande classe "Object" qui contient la méthode "toString". Il faut la surcharger dans nos classes pour qu'elle puisse retourner quelque chose par exemple.

Exemple : 
```java
package campus;

public class Magicien extends Personnage {
	public String toString()
	{
		return super.toString() + "\nSort : " + sort + "\nPhiltre : " + philtre;
	}
}
```
Infos : 
* super.toString() : fait référence à la méthode "toString" de la classe parente 
* "\n" permet d'aller à la ligne

## Gérer les erreurs - exceptions : try - catch


### try - catch 

Pour gérer les erreurs, utiliser try-catch. Dans le try se trouve le code qu'il faut essayer d'éxécuter puis dans le catch on attrape des erreurs pour pouvoir les traiter.

Par exemple, l'utilisateur doit renseigner le "Niveau de vie" d'un personnage.

Pour cela, même si dans l'idée la variable est un Entier, il faut la déclarer en String dès le début pour pouvoir dans le try-catch gérer les erreurs.

```java
//Fonction permettant de choisir le niveau de vie du personnage et qui retourne l'élément sélectionné
    private static String SelectNiveauViePerso() {
        Scanner sc = new Scanner(System.in);
        System.out.println("Quel niveau de vie souhaitez-vous donner à votre personnage (0-100) ?");
        //Initialiser une variable à "null" qui stockera ensuite le choix de l'utilisateur
        String niveauVie = null;
        //Variable pour permettre de boucler
        boolean isInteger = false;

        //Boucler tant que la variable "isInteger" est fausse
        while (!isInteger) {
            niveauVie = sc.nextLine();
            try {
              //Si la variable peut être convertie en un Entier alors on arrête la boucle
                Integer.parseInt(niveauVie);
                isInteger = true;
            } 
            catch (java.lang.NumberFormatException e) {
              //Si ce n'est pas possible relancer un message pour recommencer la saisie
                System.out.println("Erreur de saisie, renseigner une valeur entre 0 et 100");
            }
        }

        return niveauVie;
    }
```


#### 2 belles méthodes pour gérer les erreurs


```java
// Fonction permettant de convertir une chaîne de caractères en entier
    private static int ConvertStringToInteger(String str) {
        try {
            return Integer.parseInt(str);
        } catch (java.lang.NumberFormatException e) {
            return -1;
        }
    }

    //Fonction permettant de vérifier le choix de l'utilisateur et boucler tant que l'utilisateur n'a pas choisi un entier
    private static int GetUserChoice(String message) {
        int userChoice = -1;
        while (userChoice == -1) {
            Scanner sc = new Scanner(System.in);
            System.out.println(message);
            String selectPerso = sc.nextLine();
            userChoice = ConvertStringToInteger(selectPerso);
        }
        return userChoice;
    }

```


### Créer ses propres exceptions 

* Créer une classe avec l'exception : ici gérer un champ vide
```java
public class ChampVideException extends Exception {

    public ChampVideException() {
        System.out.println("Le champs ne peut être vide ! \nUn nom vous est donné par défaut");
    }
}
```

* Méthode permettant de créer un nom pour un Personnage 
 * utiliser l'exception dans la méthode : methode() throws nomException {}
 * générer l'exception : throw new ChampVideException()
```
public static String creationNom() throws ChampVideException{

  String nomPerso = sc.nextLine();
  {
    while(nomPerso.equals(""))
    {
      throw new ChampVideException();
    }
  }
  return nomPerso;
}
```

* Dans le main, utiliser un try - catch pour attribuer s'il y a l'erreur ChampVide
```java
try {

  System.out.println("Donnez-lui un nom ?");

  //Mettre à jour le nom du guerrier avec la méthode permettant de créer un Nom
  guerrier1.setNom(Saisie.creationNom());
}
catch (ChampVideException e) {
  //Attraper l'erreur et donner un nom standard au Personnage
  guerrier1.setNom("John Doe");
} 
```


## Debbuger un programme 

Utiliser le mode "Debug" de l'IDE, ici IntelliJ, qui permet d'éxécuter pas à pas le programme. 

Le système se base sur des breakpoints, des marqueurs à placer sur les lignes de code que l'on souhaite analyser.

* breakpoint : arrête le programme au début de la ligne 
* step over : exécuter la ligne 
* step into : entrer dans le processus
* clic droit - set value : modifier la valeur d'une variable
* clic droit - evaluate expression : tester une expression pour savoir ce qu'elle renvoit à l'endroit où on est dans le code
* clic droit - watch : surveiller des variables en particulier


## Les collections 

### ArrayList 

L'objet ArrayList est un objet qui n'a pas de taille limite et qui acceptent n'importe quel type de données y compris null.
Il est également possible de typer les données à l'intérieur de l'ArrayList.

#### ArrayList non typée 

```java
ArrayList al = new ArrayList();
    al.add(12);
    al.add("Une chaîne de caractères !");
    al.add(12.20f);
    al.add('d');
```

#### Déclarer une ArrayList : 

Syntaxe :
```java
ArrayList<Type de variables> nomListe = new ArrayList<Type de variables>();
```

Exemple : 
```java
ArrayList<Integer> temperatures = new ArrayList<Integer>();
```


#### Ajouter des données 

Pour ajouter des données dans la liste on utilise la méthode "add".

Syntaxe :
```java
nomArrayList.add(variable);
```

Exemple : 
```java
temperatures.add(35);
```


#### Insérer des données 

Pour insérer des données dans la liste on utilise la méthode "add" avec 2 paramètres :
* 1er : la position dans la liste
* 2ème : la valeur à ajouter

Syntaxe :
```java
nomArrayList.add(position , variable);
```

Exemple : 
```java
temperatures.add(1, 35); //ajout en 2ème position de la liste de la valeur 35
```

#### Accéder aux éléments

Il faut utiliser la position dans la liste pour accéder à l'élément avec la méthode "get". L'index commence à 0.

Syntaxe :
```java
nomArrayList.get(index);
```

Exemple : 
```java
temperatures.get(2); //accéder au 3ème élément de la liste
```


#### Boucler dans une ArrayList 

Pour afficher l'ensemble des données on utilise une boucle ainsi que la méthode "size" pour obtenir le nombre d'éléments dans la liste (retourne un entier).

**Boucler avec une boucle FOR** :
```java
for (int i = 0 ; i < nomArrayList.size() ; i++){
  System.out.println( nomArrayList.get(i) );
}
```

**Boucler avec un FOREACH** : un element dans (:) la liste d'éléments
```java
for (Integer unElement : nomArrayList){
    System.out.println(unElement);
}
```

### HashMap 

Le principe est qu'il y a une "clé" et une "valeur associée".

#### Déclarer un HashMap

Syntaxe :
```java
HashMap<type Clé, type Valeur> nomHashMap = new HashMap<type Clé, type Valeur>();
```

Par exemple : le nom d'un ami associé à son âge
```java
HashMap<String, Integer> myFriends = new HashMap<String, Integer>();
```

#### Ajouter des données 

Pour ajouter des données on utilise la méthodes "put".

Syntaxe :
```java
nomHashMap.put("clé", "valeur");
```

Exemple :
```java
myFriends.put("Mark", 24);
```


#### Insérer des données 

Pour insérer des données dans la liste on utilise la méthode "add" avec 2 paramètres :
* 1er : la position dans la liste
* 2ème : la valeur à ajouter

Syntaxe :
```java
nomArrayList.add(position , variable);
```

Exemple : 
```java
temperatures.add(1, 35); //ajout en 2ème position de la liste de la valeur 35
```

#### Accéder aux éléments

Il faut utiliser la clé pour accéder à la valeur avec la méthode "get".

Syntaxe :
```java
nomHashMap.get("clé");
```

Exemple : 
```java
myFriends.get("toto"); //accéder à la valeur de la clé "toto"
```


#### Boucler dans un HashMap

Pour afficher l'ensemble des données on utilise une boucle.

La méthode "size" permet d'obtenir le nombre de paires "key:value" du HashMap :
```java
nomHashMap.size(); //retourne le nombre de paires
```


**Boucler avec un FOREACH** : un element dans (:) la liste d'éléments
```java
for (typeClé nomClé : nomHashMap.keyset())
{
    System.out.println(nomClé);
}
```

Exemple : les plats d'un restaurant (clé) et leur prix (valeur)
```java
for (String item : restaurantMenu.keySet()) 
{
   System.out.println("A " + item + " costs " + restaurantMenu.get(item) + " dollars.");
}
```

## JavaDoc

La JavaDoc est la documentation de l'ensemble des classes de notre projet.

Exemple : 
```java
/**
     * Get nom string.
     *
     * @return the string
*/

public String getNom(){
  return nom;
}
```

### Créer la JavaDoc avec IntelliJ Idea (IDE)

Installer le Plugin dans Plugin/Browse repositories : "JavaDoc - CODE TOOLS"

#### Générer la JavaDoc dans les classes 

* shift(maj) + ctrl + alt + G : génére pour toute la classe 
* shift(maj) + alt + G : génére pour uniquement la méthode sélectionnée 
* shift(maj) + ctrl + alt + Z : supprimer la JavaDoc pour toute la classe 
* shift(maj) + alt + Z : supprimer la JavaDoc pour la méthode sélectionnée

#### Générer la documentation JavaDoc

Génére la documentation JavaDoc (fichier html, css...).

* Créer un répertoire dans le projet "javadoc" où se stockeront l'ensemble des fichiers 
* Dans Tools / Generate JavaDoc
* Cocher "Whole project" ou en cas d'erreur dans la génération cocher "Custom Scope" et choisir "Module NomProjet"
* Choisir l'emplacement où sera exportée la JavaDoc "Output directory"
* Curseur : choisir toutes les classes private...public


## Généricité 

Le principe de la généricité est de faire des classes qui acceptent un certain type d'objets ou de données de façon dynamique. 

Déclarer une classe générique :
```java
public class Solo<T> {
 
  //Variable d'instance
  private T valeur;
        
  //Constructeur par défaut
  public Solo(){
    this.valeur = null;
  }

  //Constructeur avec paramètre inconnu pour l'instant
  public Solo(T val){
    this.valeur = val;
  }
        
  //Définit la valeur avec le paramètre
  public void setValeur(T val){
    this.valeur = val;
  }
        
  //Retourne la valeur déjà « castée » par la signature de la méthode !
  public T getValeur(){
    return this.valeur;
  }       
}
```

Instancier cette classe 
```java
public static void main(String[] args) {
  Solo<Integer> val = new Solo<Integer>(12);
  int nbre = val.getValeur();             
}
```


Il est également possible d'avoir plusieurs types dynamiques 
```java
public class Duo<T, S> { 
  //Variable d'instance de type T
  private T valeur1;

  //Variable d'instance de type S
  private S valeur2;
        
  //Constructeur par défaut
  public Duo(){
    this.valeur1 = null;
    this.valeur2 = null;
  }        

  //Constructeur avec paramètres
  public Duo(T val1, S val2){
    this.valeur1 = val1;
    this.valeur2 = val2;
  }
        
  //Méthodes d'initialisation des deux valeurs
  public void setValeur(T val1, S val2){
    this.valeur1 = val1;
    this.valeur2 = val2;
  }
 
  //Retourne la valeur T
  public T getValeur1() {
    return valeur1;
  }
 
  //Définit la valeur T
  public void setValeur1(T valeur1) {
    this.valeur1 = valeur1;
  }
 
  //idem pour la valeur S
  }        
}
```

Instancier cette classe avec 2 types dynamiques
```java
public static void main(String[] args) {
  Duo<String, Boolean> dual = new Duo<String, Boolean>("toto", true);
                  
  Duo<Double, Character> dual2 = new Duo<Double, Character>(12.2585, 'C');
}
``` 


## Diagrammes : modéliser le programme

Il existe 2 grands types de diagrammes : 
* UML : modélisation des classes
* Use case : représentation des fonctionnalités du programme

Outils : 
* Visual Paradigm

### Diagrammes UML 

Le sigle « UML » signifie Unified Modeling Language, que l'on peut traduire par « langage de modélisation unifié ». 
Il ne s'agit pas d'un langage de programmation, mais plutôt d'une méthode de modélisation. La méthode Merise, par exemple, en est une autre.

Ce diagramme permet de modéliser l'ensemble des classes (classes, interfaces ...) et leurs liens. 

* -> : est une instance de cette classe 
* -> (pleine) : extends de 
* << Nom Interface >> 
* - - -> : implémente l'interface

[Vidéo Youtube uml diagramme de classe sous IntelliJ IDEA](https://www.youtube.com/watch?v=ddHXKWguxWk)


#### Les diagrammes UML sous IntelliJ Idea 

1. Créer un nouveau diagramme sous IntelliJ IDEA

    * Aller sur `File / New / Diagram / Java Class Diagram`
    * Créer dans le dossier `src` un dossier `uml`
    * Créer dans ce dossier un fichier `monfichier.uml`
    * Cliquer sur OK

2. Créer chaque classe

    * Clic droit + choisir `New / Class`
    * Saisir le `Name` + `Package`

3. Créer les attributs de la classe

    * Clic droit + choisir `New / Field`
    * Saisir les infos 
        * Visibility (Private/Protected...)
        * Type (String, int...)
        * Name
        * Initializer (Valeur par défaut)

4. Créer les méthodes

    * Aller sur la classe créée
    * Faire `Alt + Inser`
    * Choisir `getter / setter / toString...`
    * Revenir sur le fichier uml
    * Clic droit + `Show Categories / Methods`

5. Héritage

    * Clic droit `New / Line to`
    * Choisir le parent

6. Afficher le détail des classes

    * Cliquer sur les icones 
        f : Field (attributs)
        m étoile : Constructeur
        m : Méthodes

7. Exporter en format image

    * Cliquer sur icone `Export to file`
    * Choisir le type d'image souhaitée
    * Se positionner sur le dossier uml
    * Cliquer sur OK
    
#### Pour créer un diagramme UML à partir d'un projet existant

1. Créer un nouveau diagramme sous IntelliJ IDEA
   
   * Aller sur `File / New / Diagram / Java Class Diagram`
   * Créer dans le dossier `src` un dossier `uml`
   * Créer dans ce dossier un fichier `monfichier.uml`
   * Cliquer sur OK

2. Faire glisser sur la fenêtre les différentes classes créées 

3. Choisir dans le menu ce que l'on veut afficher



### Diagrammes Use Case 

Il permet d'identifier les possibilités d'interaction entre le système et les acteurs (intervenants extérieurs au système), c'est-à-dire toutes les fonctionnalités que doit fournir le système.

Acteur : 
* Il représente un élément externe (utilisateur ou système tiers) qui interagit avec le programme

Cas d'utilisation : 
* Représente une fonctionnalité du programme
* Se représente par une ellipse contenant un nom décrivant la fonctionnalité et éventuellement un stéréotype.
* Le nom du use case doit se composer d'un verbe à l'infinitif qui décrit une action. Pour que l'ensemble du modèle soit cohérent il faut choisir tous les verbes soit du point de vue du système soit du point de vue de l'utilisateur (ce qui est généralement préférable).

Relations entre cas d'utilisation : 
* L'inclusion « include » : Cela implique obligatoirement l'inclusion d'un cas d'utilisation dans un autre comme ici « Retire argent » fait obligatoirement appel à « S'authentifier ».
* L'extension « extended » : Cela permet éventuellement l'extension d'un cas d'utilisation par un autre comme ici « Vérifier solde » peut étendre « Effectuer virement ».
* Le point d'extension : Il est possible de préciser exactement à quel moment une extension est appelée comme ci-dessous par un « Extension points » ici « verification_solde {après avoir demandé le montant}.
* La condition d'extension : Il est possible d'ajouter en note sous quelle condition l'extension doit se produire comme ci-dessous si le montant est supérieur à 20€.
* L'héritage : Il permet de définir la spécialisation d'un cas d'utilisation comme ici consulter un compte depuis le DAB ou consulter le compte depuis Internet.

[Exemple](http://www.uml-sysml.org/diagrammes-uml-et-sysml/diagramme-uml/use-case-diagramme)


## Design Pattern

Modèle de conception, permet de générer les comportements dynamiques. 

Utilisation d'interfaces et de classes venant implémenter ces interfaces.

[Exemple sur GIT Test_Interfaces](https://github.com/MarionChapuis/Test_Interfaces)

*Exemple :*
Avoir un comportement "Combattre" différent selon le type d'Arme utilisée. 
Par exemple, afficher "je combat avec une épée" si le personnage a une épée, ou "Je tire à l'arc" s'il utilise un arc.

* Création d'une interface "Esprit Combatif" comprenant une méthode "Combat()" qui sera implémentée 
```java
public interface EspritCombatif {
    public void Combat();
}
```

* Création de classes "CombatArc" et "CombatEpee" qui vont implémenter l'interface 
```java
public class CombatArc implements EspritCombatif {

    @Override
    public void Combat() {
        System.out.println("Je tire à l'arc");
    }
}
```

* Création d'une classe Personnage qui va également implémenter l'interface
   * Attribut 'e' du type de l'interface 'EspritCombatif' qui contiendra l'instance d'une des classes "CombatEpee" ou "CombatArc"
   * La classe implémente la méthode Combat () en utilisant la méthode Combat() de son attribut dynamique 'e'
   * Dans l'exemple ci-dessous, e.Combat() correspond à la méthode Combat de la classe "CombatEpee"
```java
public class Personnage implements EspritCombatif {

    EspritCombatif e = new CombatEpee();

    public Personnage(){
    }

    @Override
    public void Combat() {
        e.Combat();
    }
}
```

* Dans le main, instancier un personnage et afficher la méthode Combat selon l'Arme utilisée 
```java
public class Main {

    public static void main(String[] args) {

        Personnage perso = new Personnage();
        perso.Combat(); //retournera "je combat avec une épée" car dans la Classe Personnage, l'attribut e = new CombatEpee()

        perso.e = new CombatArc(); //modifier l'attribut 'e' (avec un setter c'est mieux) 
        perso.Combat(); //retournera "Je tire à l'arc" 
    }
}
```




## JDBC : accès aux bases de données 

[OpenClassRooms JDBC](https://openclassrooms.com/courses/apprenez-a-programmer-en-java/jdbc-la-porte-d-acces-aux-bases-de-donnees)

JDBC : Java DataBase Connectivity

Pour utiliser une BDD, vous avez besoin de deux éléments : la base de données et ce qu'on appelle le SGBD (Système de Gestion de Base de Données).

### Se connecter à une BDD

Pour se connecter avec Java à une BDD, il faut un fichier ".jar" qui est un driver.

* Ce fichier ".jar" est à télécharger avec une belle recherche Google : pilote JDBC + postGreSQL(ou mysql...) : [lien fichier zip](https://dev.mysql.com/downloads/connector/j/)
* Ajouter le fichier "xxxxx-bin.jar", il existe 2 solutions : 
  * L'inclure dans votre projet et l'ajouter au CLASSPATH (à favoriser si l'application est vouée à être exportée sur d'autres postes)
  * ou 
  * Le placer dans le dossier "Java/lib/ext" présent dans le dossier d'installation du JRE.
* Faire le lien dans le 'main' 

* Code pour le lien avec PostGreSQL :
```java
import java.sql.Connection;
import java.sql.DriverManager;

public static void main(String[] args) {      
    try {
      Class.forName("org.postgresql.Driver");
      System.out.println("Driver O.K.");

      String url = "jdbc:postgresql://localhost:5432/NomBDD";
      String user = "postgres";
      String passwd = "postgres";

      Connection conn = DriverManager.getConnection(url, user, passwd);
      System.out.println("Connexion effective !");         
         
    } catch (Exception e) {
      e.printStackTrace();
    }      
  }
```

* Code pour le lien avec MySQL :
```java
import java.sql.Connection;
import java.sql.DriverManager;

public static void main(String[] args) {
        try {
            Class.forName("com.mysql.jdbc.Driver");
            System.out.println("Driver O.K.");

            String url = "jdbc:mysql://localhost:3306/NomBDD";
            String user = "root";
            String passwd = "";

            Connection conn = DriverManager.getConnection(url, user, passwd);
            System.out.println("Connexion effective !");

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
*A noter, le '3306'* est indiqué dans PhpMyAdmin 'serve XXXX'

L'url se compose de la manière suivante :
* "jdbc:"
* "localhost:" nom de la machine
* nom de la BDD

**Avec IDE IntelliJ** 
* File / Project Structure 
* Modules
* Dependencies
* Tout à droite : '+' "Jars or directories"
* Selectionner le fichier dans "jre/bin/ext/...bin.jar"

### IMPERATIF : Utiliser le Pattern Singleton 

Il s'agit d'une bonne pratique afin d'utiliser un seul "câble" de connexion lors des différentes connexions à la BDD pour effectuer des requêtes. 

* Créer une classe final 
* 1 attribut static public du type de la Classe 
* 1 attribut private de type "Connection" ainsi que son getter 
* 1 méthode static retournant un objet du type de la Classe vérifiant si une connexion a déjà été établie et retourne la connexion (s'il n'existe pas de connexion alors elle instancie une nouvelle connexion)
* 1 constructeur contenant un try catch avec la connexion à la BDD (user, password, drive..)

Lorsqu'on souhaite se connecter à la BDD créer une variable de type "Connection" qui appelle la méthode static puis le getter de la connexion

Classe contenant la connexion 
```java
import java.sql.Connection;
import java.sql.DriverManager;

public final class Connect {

    public static Connect connection;
    private  Connection conn = null;

    public  Connection getConn() {
        return conn;
    }


    public static Connect getInstance()
    {
        if (connection==null)
        {
            connection = new Connect();
        }
        return connection;
    }


    public Connect() {
        try {
            Class.forName("com.mysql.jdbc.Driver");
            System.out.println("Driver O.K.");

            String url = "jdbc:mysql://localhost:3306/testconnect";
            String user = "root";
            String passwd = "";

            conn = DriverManager.getConnection(url, user, passwd);
        }
        catch (Exception e)
        {
            System.out.println("echec de la connexion");
        }
    }
}
```

Utilisation de la connexion 
```java
public static void main(String[] args) {
  try {
    //Ouvrir une connexion à la BDD
     Connection conn = Connect.getInstance().getConn();

    //Effectuer les requêtes 
    
   }
   catch (Exception e) {
    e.printStackTrace();
  }
}
```


### Fouiller dans la BDD

Les grandes étapes : 
* création de l'objet Statement : permet d'exécuter des instructions SQL
* exécution de la requête SQL 
* récupération et affichage des données via l'objet ResultSet : permet de stocker les données 
* fermeture des objets utilisés (bien que non obligatoire, c'est recommandé)

Il est possible d'utiliser l'objet **ResultSetMetaData** qui permet de récupérer des infos utiles :
* le nombre de colonnes d'un résultat ;
* le nom des colonnes d'un résultat ;
* le type de données stocké dans chaque colonne ;
* le nom de la table à laquelle appartient la colonne (dans le cas d'une jointure de tables) ;
* ...
Il existe aussi un objet DataBaseMetaData qui fournit des informations sur la base de données.

**Attention : les indices de colonnes SQL commencent à 1 contrairement aux indices de tableaux**

#### Afficher les données 

*Exemple : ce code est dans le "Try"*

```java
//Création d'un objet Statement
Statement state = conn.createStatement();

//L'objet ResultSet contient le résultat de la requête SQL
ResultSet resultat = state.executeQuery("SELECT * FROM personnages");

//On récupère les MetaData
ResultSetMetaData resultMeta = resultat.getMetaData();

System.out.println("\n**************");

//On affiche le nom des colonnes
for(int i = 1; i <= resultMeta.getColumnCount(); i++) {
  System.out.print("\t" + resultMeta.getColumnName(i).toUpperCase() + "\t *");
}
System.out.println("\n**************");

//On affiche les résultats
while(resultat.next()) {

  for (int i = 1; i <= resultMeta.getColumnCount(); i++){
    System.out.print("\t" + resultat.getObject(i).toString() + "\t |");
  }

  System.out.println("\n---------------------------------");
}

//On ferme les objets utilisés
resultat.close();
state.close();
```

La méthode next() permet de positionner l'objet sur la ligne suivante de la liste de résultats.

Lorsque l'on connait le type de données que l'on récupère le code peut être le suivant :
```java
while(result.next()){
  System.out.print("\t" + result.getInt("id") + "\t |");
  System.out.print("\t" + result.getString("nom") + "\t |");
  System.out.println("\n---------------------------------");
}
```

| Méthodes GetXXX() |
|-------------------|
|getArray(int colummnIndex) |
|getAscii(int colummnIndex) |
|getBigDecimal(int colummnIndex) |
|getBinary(int colummnIndex) |
|getBlob(int colummnIndex) |
|getBoolean(int colummnIndex) |
|getBytes(int colummnIndex) |
|getCharacter(int colummnIndex) |
|getDate(int colummnIndex) |
|getDouble(int colummnIndex) |
|getFloat(int colummnIndex) |
|getInt(int colummnIndex) |
|getLong(int colummnIndex) |
|getObject(int colummnIndex) |
|getString(int colummnIndex) |


#### Faire des requêtes avec liaisons et tris

```java
String query = "SELECT prof_nom, prof_prenom, mat_nom, cls_nom FROM professeur";
query += " INNER JOIN j_mat_prof ON jmp_prof_k = prof_id";
query += " INNER JOIN matiere ON jmp_mat_k = mat_id";
query += " INNER JOIN j_cls_jmp ON jcm_jmp_k = jmp_id";
query += " INNER JOIN classe ON jcm_cls_k = cls_id AND cls_id IN(1, 7)";
query += " ORDER BY cls_nom DESC, prof_nom";

ResultSet result = state.executeQuery(query);
```


#### Statement 

Lors de la création de Statement via createStatement(), il est possible d'ajouter des paramètres :

Le premier paramètre est utile pour la lecture du jeu d'enregistrements :

TYPE_FORWARD_ONLY : le résultat n'est consultable qu'en avançant dans les données renvoyées, il est donc impossible de revenir en arrière lors de la lecture ;

TYPE_SCROLL_SENSITIVE : le parcours peut se faire vers l'avant ou vers l'arrière et le curseur peut se positionner n'importe où, et si des changements surviennent dans la base pendant la lecture, ils seront directement visibles lors du parcours des résultats ;

TYPE_SCROLL_INSENSITIVE : à la différence du précédent, les changements ne seront pas visibles.

Le second concerne la possibilité de mise à jour du jeu d'enregistrements :

CONCUR_READONLY : les données sont consultables en lecture seule, c'est-à-dire que l'on ne peut modifier des valeurs pour mettre la base à jour ;

CONCUR_UPDATABLE : les données sont modifiables ; lors d'une modification, la base est mise à jour.

Par défaut, les ResultSet issus d'un Statement sont de type TYPE_FORWARD_ONLY pour le parcours et CONCUR_READONLY pour les actions réalisables.

*Exemple*
```java
Statement state = conn.createStatement(ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_UPDATABLE);
```


#### Les requêtes préparées 

A la place de Statement, il est possible d'utiliser PreparedStatement qui contient 2 avantages :
* la requête SQL est précompilé ce qui permet de gagner du temps d'éxécution dans le moteur SQL de la BDD
* il est possible d'utiliser des paramètres à trous

*Exemple* :
```java
//On crée la requête
String query = "SELECT prof_nom, prof_prenom FROM professeur";

//Premier trou pour le nom du professeur
query += " WHERE prof_nom = ?";

//Deuxième trou pour l'identifiant du professeur
query += " OR prof_id = ?";

//On crée l'objet avec la requête en paramètre
PreparedStatement prepare = conn.prepareStatement(query);

//On remplace le premier trou par le nom du professeur
prepare.setString(1, "MAMOU");

//On remplace le deuxième trou par l'identifiant du professeur
prepare.setInt(2, 2);

//On affiche la requête exécutée
System.out.println(prepare.toString());

//On modifie le premier trou
prepare.setString(1, "TOTO");

//On affiche à nouveau la requête exécutée
System.out.println(prepare.toString());

//On modifie le deuxième trou
prepare.setInt(2, 159753);

//On affiche une nouvelle fois la requête exécutée
System.out.println(prepare.toString());

prepare.close();
state.close();
```

Ici on utilise "prepare.setXXX" pour pouvoir indiquer les trous.

Pour en terminer avec les méthodes de l'objet PreparedStatement, prepare.clearParameters() permet de réinitialiser la requête préparée afin de retirer toutes les valeurs renseignées.

*Exemple : table 'personnages' afficher un personnage spécifique*
```java
//Afficher un perso en particulier
System.out.println("Indiquer l'id du perso à afficher :");
Scanner sc = new Scanner(System.in);
int choix = sc.nextInt();
System.out.println("vous avez sélectionné : " + choix);

String query = "SELECT * FROM personnages";
query+= " WHERE id = ?";

//Creation de l'objet avec la requête en paramètre
PreparedStatement prepare = conn.prepareStatement(query);

//Remplacer le trou par le choix de l'utilisateur
prepare.setInt(1, choix);

//Afficher la requête
System.out.println(prepare.toString());

//L'objet ResultSet contient le résultat de la requête SQL
ResultSet resultat = prepare.executeQuery();
//On récupère les MetaData
ResultSetMetaData resultMeta = resultat.getMetaData();

//On affiche le nom des colonnes
for (int i = 1; i <= resultMeta.getColumnCount(); i++)
System.out.print("\t" + resultMeta.getColumnName(i).toUpperCase() + "\t |");

System.out.println("\n------------------------------------------------------------------------------------------------------------------");

//On affiche les infos des colonnes 
while (resultat.next()) {
  for (int i = 1; i <= resultMeta.getColumnCount(); i++)
  System.out.print("\t" + resultat.getObject(i).toString() + "\t |");
  System.out.println("\n------------------------------------------------------------------------------------------------------------------");
}

resultat.close();
prepare.close();
```



#### ResultSet 

L'objet ResultSet offre beaucoup de méthodes permettant d'explorer les résultats, à condition d'avoir bien préparé l'objet Statement.

| objectif | méthode |
|----------|:--------:|
|vous positionner avant la première ligne de votre résultat | res.beforeFirst() ;
|savoir si vous vous trouvez avant la première ligne | res.isBeforeFirst() ;
|vous placer sur la première ligne de votre résultat | res.first() ;
|savoir si vous vous trouvez sur la première ligne | res.isFirst() ;
|vous retrouver sur la dernière ligne | res.last() ;
|savoir si vous vous trouvez sur la dernière ligne | res.isLast() ;
|vous positionner après la dernière ligne de résultat | res.afterLast() ;
|savoir si vous vous trouvez après la dernière ligne | res.isAfterLast() ;
|aller de la première ligne à la dernière | res.next() ;
|aller de la dernière ligne à la première | res.previous() ;
|vous positionner sur une ligne précise de votre résultat | res.absolute(5) ;
|vous positionner sur une ligne par rapport à votre emplacement actuel | res.relative(-3)


### Modifier les données 

Pour remplacer les données, on remplace getXXX() par updateXXX(String nomColonne, valeur à attribuer).

* MAJ : monResultat.updateString("nom", "Chapuis");
* Validation MAJ : monResultat.updateRow();

* Annuler des changements : cancelRowUpdates(); **A faire avant la méthode de validation**

*Exemple : modifier les infos d'un personnage*
```java
//---------------------------------------------------Modifier les infos d'un perso--------------------------------------------------------
//Creation de l'objet avec la requête en paramètre
Statement state = conn.createStatement(ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_UPDATABLE);

//Selectionner une ligne dans la BDD
String query = "SELECT * FROM personnages " + "WHERE id = 1";
ResultSet resultat = state.executeQuery(query);
//Se position sur le résultat
resultat.first();

//Afficher la ligne
System.out.println("---------------------Avant modif --------------------------------");
System.out.println("Nom : " + resultat.getString("nom") + "\nImage : " + resultat.getString("image"));

//Mettre à jour les champs
resultat.updateString("nom", "Coin coin junior");
resultat.updateString("image", "Super coin coin junior");
resultat.updateString("bouclier", "Une plume magique");

//On valide les modifications
resultat.updateRow();

//Afficher les modifications
System.out.println("---------------------Après modif --------------------------------");
System.out.println("Nom : " + resultat.getString("nom") + "\nImage : " + resultat.getString("image") + "\nBouclier : " + resultat.getString("bouclier"));

//On ferme 
resultat.close();
state.close();
```


### Insérer, Supprimer .. les données 

Les objets Statement sont chargés d'éxécuter les instructions SQL. Les requêtes INSERT, UPDATE, DELETE, CREATE sont exécutées par ces objets.

*Exemple* ajouter un perso dans la BDD 

```java
//Création de l'objet
Statement state = conn.createStatement();

//Ajouter la ligne 
state.executeUpdate("INSERT INTO personnages (id, type, niveauVie, nom, image, niveauAttaque, objetAttaque, bouclier) VALUES (NULL, 'Guerrier', '150', 'Romain', 'Un ptit Romain', '55', 'Arme', 'Humour atypique')");

//L'objet ResultSet contient le résultat de la requête SQL pour affiche l'ensemble des personnages
ResultSet liste = state.executeQuery("SELECT * FROM personnages");

//On récupère les MetaData
ResultSetMetaData resultMeta = liste.getMetaData();

System.out.println("\n------------------------------------------------------------------------------------------------------------------");
//On affiche le nom des colonnes
for (int i = 1; i <= resultMeta.getColumnCount(); i++) {
  System.out.print("\t" + resultMeta.getColumnName(i).toUpperCase() + "\t |");
}
System.out.println("\n------------------------------------------------------------------------------------------------------------------");

//On affiche les infos de la BDD
while (liste.next()) {
  for (int i = 1; i <= resultMeta.getColumnCount(); i++) {
    System.out.print("\t" + liste.getObject(i).toString() + "\t |");
  }
  System.out.println("\n------------------------------------------------------------------------------------------------------------------");
}

//On ferme
state.close();
liste.close();
```


## Insérer, modifier des données avec des requêtes préparées 

*Exemple : ajouter un personnage avec les infos de l'utilisateur* 
```java
//---------------------------------------------------Créer un personnage avec la console--------------------------------------------------------

Scanner sc = new Scanner(System.in);

System.out.println("Nom du perso ? ");
String nom = sc.nextLine();

System.out.println("Image ? ");
String image = sc.nextLine();

System.out.println("Bouclier ? ");
String bouclier = sc.nextLine();

Guerrier guerrier = new Guerrier(nom, image, bouclier);

//La requête d'insertion
String query = "INSERT INTO personnages (id, type, niveauVie, nom, image, niveauAttaque, objetAttaque, bouclier) VALUES (NULL, ?, ?, ?, ?, ?, ?, ?)";

//Exécution de la requête préparée
PreparedStatement state = conn.prepareStatement(query);

//Remplacer les ?
state.setString(1,guerrier.getType());
state.setInt(2, guerrier.getNiveauVie());
state.setString(3,guerrier.getNom());
state.setString(4, guerrier.getImage());
state.setInt(5, guerrier.getNiveauAttaque());
state.setString(6, guerrier.getObjetAttaque());
state.setString(7, guerrier.getBouclier());

//Exécuter la mise à jour 
state.executeUpdate();

//Afficher la liste des personnages

//L'objet ResultSet contient le résultat de la requête SQL
ResultSet liste = state.executeQuery("SELECT * FROM personnages");

//On récupère les MetaData
ResultSetMetaData resultMeta = liste.getMetaData();

System.out.println("\n------------------------------------------------------------------------------------------------------------------");
//On affiche le nom des colonnes
for (int i = 1; i <= resultMeta.getColumnCount(); i++) {
  System.out.print("\t" + resultMeta.getColumnName(i).toUpperCase() + "\t |");
}
System.out.println("\n------------------------------------------------------------------------------------------------------------------");

//On affiche les infos de la BDD
while (liste.next()) {
  for (int i = 1; i <= resultMeta.getColumnCount(); i++) {
    System.out.print("\t" + liste.getObject(i).toString() + "\t |");
  }
  System.out.println("\n------------------------------------------------------------------------------------------------------------------");
}

state.close();
liste.close();
```




## Synthèse Méthodes 

| Méthodes | Fonction | Exemple 
| :-------:|---------|---------
| Integer.parseInt(String variable) | Convertir un chaîne de caractères en une entier | int maVariableInt = Integer.parseInt("1");
| equals("String variable") | Comparer une chaîne de caractères | String maVar = "Oui" ; maVar.equals("Non")  
