# Java

[Super mémo Java](http://thierry-leriche-dessirier.developpez.com/tutoriels/java/mots-cles-java/#LIV-B-9)

## Définition & Installation

JAVA est un langage compilé et typé.

JDK : Java Development Kit 

JRE : Java Environment Execution

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


### Installer Maven 

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

Créer une interface :
```java
public interface Bonjour{

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

## Gérer les erreurs : try - catch

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

## Les collections 

### ArrayList 

L'objet ArrayList est un objet qui n'a pas de taille limite et qui acceptent n'importe quel type de données y compris null.
Il est également possible de typer les données à l'intérieur de l'ArrayList.

##### ArrayList non typée 

```java
ArrayList al = new ArrayList();
    al.add(12);
    al.add("Une chaîne de caractères !");
    al.add(12.20f);
    al.add('d');
```

##### Déclarer une ArrayList : 

Syntaxe :
```java
ArrayList<Type de variables> nomListe = new ArrayList<Type de variables>();
```

Exemple : 
```java
ArrayList<Integer> temperatures = new ArrayList<Integer>();
```


##### Ajouter des données 

Pour ajouter des données dans la liste on utilise la méthode "add".

Syntaxe :
```java
nomArrayList.add(variable);
```

Exemple : 
```java
temperatures.add(35);
```


##### Insérer des données 

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

##### Accéder aux éléments

Il faut utiliser la position dans la liste pour accéder à l'élément avec la méthode "get". L'index commence à 0.

Syntaxe :
```java
nomArrayList.get(index);
```

Exemple : 
```java
temperatures.get(2); //accéder au 3ème élément de la liste
```


##### Boucler dans une ArrayList 

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

##### Déclarer un HashMap

Syntaxe :
```java
HashMap<type Clé, type Valeur> nomHashMap = new HashMap<type Clé, type Valeur>();
```

Par exemple : le nom d'un ami associé à son âge
```java
HashMap<String, Integer> myFriends = new HashMap<String, Integer>();
```

##### Ajouter des données 

Pour ajouter des données on utilise la méthodes "put".

Syntaxe :
```java
nomHashMap.put("clé", "valeur");
```

Exemple :
```java
myFriends.put("Mark", 24);
```


##### Insérer des données 

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

##### Accéder aux éléments

Il faut utiliser la clé pour accéder à la valeur avec la méthode "get".

Syntaxe :
```java
nomHashMap.get("clé");
```

Exemple : 
```java
myFriends.get("toto"); //accéder à la valeur de la clé "toto"
```


##### Boucler dans un HashMap

Pour afficher l'ensemble des données on utilise une boucle.

La méthode "size" permet d'obtenir le nombre de paires "key:value" du HashMap :
```java
nomHashMap.size(); //retourne le nombre de paires
```


**Boucler avec un FOREACH** : un element dans (:) la liste d'éléments
```java
for (typeClé nomClé : nomHashMap.keyset())
{
    System.out.println(unElement);
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

#### Créer la JavaDoc avec IntelliJ Idea (IDE)

Installer le Plugin dans Plugin/Browse repositories : "JavaDoc - CODE TOOLS"

##### Générer la JavaDoc dans les classes 

* shift(maj) + ctrl + alt + G : génére pour toute la classe 
* shift(maj) + alt + G : génére pour uniquement la méthode sélectionnée 
* shift(maj) + ctrl + alt + Z : supprimer la JavaDoc pour toute la classe 
* shift(maj) + alt + Z : supprimer la JavaDoc pour la méthode sélectionnée

##### Générer la documentation JavaDoc

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


## UML 

Le sigle « UML » signifie Unified Modeling Language, que l'on peut traduire par « langage de modélisation unifié ». 
Il ne s'agit pas d'un langage de programmation, mais plutôt d'une méthode de modélisation. La méthode Merise, par exemple, en est une autre.





## Synthèse Méthodes 

| Méthodes | Fonction | Exemple 
| :-------:|---------|---------
| Integer.parseInt(String variable) | Convertir un chaîne de caractères en une entier | int maVariableInt = Integer.parseInt("1");
