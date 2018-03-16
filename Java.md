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
	* mainClass : fichier principal où on mettre tout
	* artifactId : version.jar
* Coder en mettant les fichiers java dans 'hello'
* Utiliser Maven :
```bash
mvn compile
mvn install
java -cp target/<artifactId> <mainClass>
```
* Créer le Read.me et GIT 

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

**Formatage des nombres depuis Java 7**

Utilisation de l'underscore.


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
}
```

