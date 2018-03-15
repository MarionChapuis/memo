# Java

## Définition & Installation

Langage compilé et typé.

JDK : Java Development Kit 

JRE : Java Environment Execution

Le code est exécuté par une machine virtuelle grâce au JRE et JDK.

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


Dans le fichier HelloWorld (le mainClass) :
```java
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


