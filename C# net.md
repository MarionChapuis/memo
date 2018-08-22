# C# .net

### Liens

* [Cours OpenClassRooms](https://openclassrooms.com/fr/courses/218202-apprenez-a-programmer-en-c-sur-net)
* [Documentation .NET](https://docs.microsoft.com/fr-fr/dotnet/standard/)
* [Documentation c#](https://docs.microsoft.com/fr-fr/dotnet/csharp/tour-of-csharp/)
* [Guide programmation c#](https://docs.microsoft.com/fr-fr/dotnet/csharp/programming-guide/index)


### Définitions

##### C\#

Language de programmation orienté objet récent (début 2000) inspiré de Java (donc typé) et développé par Microsoft. C'est le langage recommandé pour développer sous Windows. 

##### .NET

C'est le framework ou environnement d'exécution (aussi écrit Dot NET) pour programmer en C# sous Windows : accès réseau, création de fenêtres, appel à une base de données... 

Pour développer sous MacOS ou Linux il faut utiliser .NET Core. 


### Fonctionnement C\#

C# est un langage proche de Java. 
Le framework .NET regroupe un ensemble de bibliothèques pour faciliter le développement. 

La compilation permet de traduire le code en source binaire. Mais la compilation en C# a une particularité. 

La compilation en C# ne donne pas un programme binaire, contrairement au C et au C++. Le code C# est en fait transformé dans un langage intermédiaire (appelé CIL ou MSIL) que l'on peut ensuite distribuer à tout le monde. Ce code, bien sûr, n'est pas exécutable lui-même, car l'ordinateur ne comprend que le binaire.

Le code en langage intermédiaire (CIL) correspond au programme qui sera distribué. Sous Windows, il prend l'apparence d'un .exe comme les programmes habituels, mais il ne contient en revanche pas de binaire.


![Compilation](c-sharp/Schema_compilation_c_sharp.png)

Lorsqu'on exécute le programme CIL, celui-ci est lu par un autre programme (une machine à analyser les programmes, appelée CLR) qui le compile cette fois en vrai programme binaire.
Le CLR permet également de vérifier le code (sécurité).


### Gestionnaire de packages NuGet 

NuGet est un gestionnaire de packages.


### Paramètrer l'IDE : Visual Studio

Utilisation de l'IDE Visual Studio 2017. 

* Lors du choix du fond de couleurs et du paramètre de développement choisir : "Visual C#"

Quelques raccourcis utiles :

| Raccourcis | Résultats |
| :-------------: |-------------- | 
| ctrl + k et ctrl + c | Commenter 
| ctrl + k et ctrl + u | Décommenter
| ctrl + k et ctrl + d | Indenter 


### Créer une solution C\# .net 

Dans l'IDE Visual Studio 2017 : 
* Fichier / Nouveau / Projet 
* Chosir 'Application console (.NET Framework)'
* Nommer le projet et choisir l'emplacement 
* Utiliser ensuite le Main


### Variables

![Types de base](c-sharp/variables.png)

* Une **chaîne de caractères** se trouve entre `guillemets ( " )`.
* Un **caractère** se trouve entre des `apostrophes ( ' )`.
```
"Chaîne de caractères" et 'C'
```
* Une variable doit être déclarée en indiquant devant son Type (boolean, integer, string...) et en l'initialisant : 
```c#
String MaVariable = "Caracteres";
```
* En .NET tous les types de variables (String, Int) commence par une majuscule : String, Int, Boolean...


### Enumérations

Comme en Java, il est possible de créer des énumérations qui permettent de regrouper un ensemble de valeurs de type unique. 

*Exemple :*
```c#
enum Jours
{
    Lundi,
    Mardi,
    Mercredi,
    Jeudi,
    Vendredi,
    Samedi,
    Dimanche
}
```
Les énumérations peuvent être appelées par la suite dans le code : 
```c#
Jours monJour = Jours.Vendredi;
```


### Opérateurs

| Opérateur           | Définition        | 
|:-------------------: |:------------------: | 
| <     |plus petit que 
| <=    |plus petit ou égal à
| >     |plus grand que
| >=    |plus grand ou égal à
| ==    |égal à
| !=    |différent de
| &&    |et
| \|\|  |ou


### Tableaux 

Syntaxe : 
```c#
string[] jours = new string[] { "Lundi", "Mardi", "Mercredi", "Jeudi", "Vendredi", "Samedi", "Dimanche" };
Console.WriteLine(jours[3]); // affiche Jeudi
Console.WriteLine(jours[0]); // affiche Lundi
Console.WriteLine(jours[10]); // provoque une erreur d'exécution car l'indice n'existe pas
```

Trier rapidement un tableau : 
```c#
Array.Sort(jours);
```

### Listes

Syntaxe : 
```c#
List<int> chiffres = new List<int>(); // création de la liste
chiffres.Add(8); // chiffres contient 8
chiffres.Add(9); // chiffres contient 8, 9
chiffres.Add(4); // chiffres contient 8, 9, 4

//Récupérer la position d'un élément dans une liste
int indice = jours.IndexOf(4); // indice vaut 2

//Supprimer un élément par sa position dans la liste
chiffres.RemoveAt(1); // chiffres contient 8, 4

//Parcourir une liste
foreach (int chiffre in chiffres)
{
    Console.WriteLine(chiffre);
}
```


### Boucles

#### FOR 

```c#
String[] jours = new String[] { "Lundi", "Mardi", "Mercredi", "Jeudi", "Vendredi", "Samedi", "Dimanche" };

int indice;
for (indice = 0; indice < jours.Length; indice++)
{
    Console.WriteLine(jours[indice]);
}
```

#### FOREACH

```c#
String[] jours = new String[] { "Lundi", "Mardi", "Mercredi", "Jeudi", "Vendredi", "Samedi", "Dimanche" };

foreach (String jour in jours)
{
    Console.WriteLine(jour);
}
```


#### WHILE 

```c#
int i = 0;
while (i < 50)
{
    Console.WriteLine("Bonjour C#");
    i++;
}
```

#### DO WHILE 

```c#
int i = 0;
do
{
    Console.WriteLine("Bonjour C#");
    i++;
}
while (i < 50);
```

#### Les instructions : BREAK - CONTINUE

Il est possible de sortir prématurément d’une boucle grâce à l’instruction break. Dès qu’elle est rencontrée, elle sort du bloc de code de la boucle. L’exécution du programme continue alors avec les instructions situées après la boucle. Par exemple : 

```c#
int i = 0;
while (true)
{
    if (i >= 50)
    {
        break;
    }
    Console.WriteLine("Bonjour C#");
    i++;
}
```

Il est également possible de passer à l’itération suivante d’une boucle grâce à l’utilisation du mot-clé continue. Exemple :
```c#
for (int i = 0; i < 20; i++)
{
    if (i % 2 == 0)
    {
        continue;
    }
    Console.WriteLine(i);
}
//L'exemple n'affichera que les chiffres impairs car s'il tombe sur un chiffre paire il passera à l'itération suivante et donc n'affichera pas le chiffre pair.
```


### Le Main 

Point d'entrée d'un programme exécutable (c'est l'endroit où le contrôler du programme commence et se termine).
```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Helloworld
{
    class Program
    {
        static void Main(string[] args)
        {
            System.Console.WriteLine(message.GetHelloMessage());           
        }
    }
}
```


### Propriétés

[Doc Propriétés](https://docs.microsoft.com/fr-fr/dotnet/csharp/programming-guide/classes-and-structs/properties)

Hybride entre attribut et méthode possédant des getters et setters. Il est possible de rendre le setter en visibilité 'private'.

Les propriétés permettent à une classe d'exposer un moyen public d'obtenir et de définir des valeurs, tout en masquant le code d'implémentation ou de vérification.

Dans les setters, le mot clé "value" correspond à ce que l'utilisateur entrera en paramètre du setter comme nouvelle valeur pour l'attribut. 


*Exemple* :
```c#
using System;

public class Person
{
   private string firstName;
   private string lastName;
   
   public Person(string first, string last)
   {
      firstName = first;
      lastName = last;
   }

   //Exemple d'une propriété
   public string Name => $"{firstName} {lastName}";   

   //Autre exemple d'une propriété
   public String Name
   {
        get => name;
        set => name = value;
   }
}

public class Example
{
   public static void Main()
   {
      var person = new Person("Camille", "Onette"); 
      Console.WriteLine(person.Name);
      // résultat "Camille Onette"
   }
}
```

*Exemple* : 
La méthode GetHelloMessage peut être une propriété 

```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Helloworld
{
    public class Message
    {
        //Attributs déterminant les différentes tranches horaires
        protected int matin = 9;
        protected int midi = 13;
        protected int soir = 18;

        //Propriété GetHelloMessage
        public String GetHelloMessage
        {
            get
            {
                //Récupérer la date actuelle
                DateTime date = DateTime.Now;
                //date = new DateTime(2018, 08, 20, 8, 52, 12);
                String message = "";
                //Pour la tranche vendredi soir au lundi matin
                if (date.DayOfWeek == DayOfWeek.Friday && date.Hour >= this.soir || date.DayOfWeek == DayOfWeek.Saturday || date.DayOfWeek == DayOfWeek.Sunday || date.DayOfWeek == DayOfWeek.Monday && date.Hour < this.matin)
                {
                    message = "Bon week-end";
                }
                else if (date.Hour >= this.soir || date.Hour < this.matin)
                {
                    //Tranche "semaine" pour le soir
                    message = "Bonsoir";
                }
                else if (date.Hour < this.midi)
                {
                    //Tranche "semaine" pour le matin
                    message = "Bonjour";
                }
                else
                {
                    //Tranche "semaine" pour l'après-midi
                    message = "Bon après-midi";
                }

                //Message complet  
                String messageComplet = message + " " + Environment.UserName;
                return messageComplet;
            }
        }

        //Constructeur prenant en paramètres les différentes tranches horaires
        public Message (int matin, int midi, int soir)
        {
            this.matin = matin;
            this.midi = midi;
            this.soir = soir;
        }

    }
}
```


### Tests Unitaires 

Créer un test unitaire : se positionner dans la classe, faire clic droit et sélectionner "Créer des tests unitaires".

**Attention : la classe doit être "public"**

Lorsqu'on test une classe elle est très souvent liée à d'autres classes ou d'autres éléments externes (lien avec une API). 
Pour pouvoir maîtriser les éléments externes à la classe, nous avons besoind de l'injection de dépendance. 


### Injections de dépendances et doublure de tests

L'injection de dépendance permet d'isoler les éléments externes à la classe pour pouvoir les gérer. 

La doublure de tests fait suite à l'injection de dépendance et permet d'utiliser des interfaces pour créer de "faux" objets pour simuler une dépendance lors des tests unitaires. 

Ces objets doubles sont classés en plusieurs catégories selon leur degré d'intelligence et selon la manière donc ils vont imiser le comportement de la classe remplacée.

Dans l'exemple ci-dessous, ces objets seront utilisés dans la classe FakeTime qui implémente l'interface ITime. Ils permettront d'implémenter la propriété "Date" de l'interface. 


#### Dummy

Il s'agit du plus simple (niveau degré d'intelligence), c'est une classe dont on se fiche comment elle est utilisée. 

Le Dummy est juste là pour implémenter l'interface sans logique spécifique. 

Dans l'exemple ci-dessous, le dummy correspondrait à un simple "new DateTime()" dans la classe "FakeTime" : 
```c#
namespace HelloworldTests
{
    public class FakeTime : ITime
    {
        public DateTime Date
        {
            get
            {
                return new DateTime();
            }
        }
    }
}
```

#### Stub

Alors pour les stubs, il s’agit d’implémenter une classe qui va répondre exactement ce que j’attends.

Dans l'exemple ci-dessous, dans la classe "FakeTime", le stub correspond à une date précise "new DateTime(2018,08,20,15,12,11)" : 
```c#
namespace HelloworldTests
{
    public class FakeTime : ITime
    {
        public DateTime Date
        {
            get
            {
                return new DateTime(2018,08,20,15,12,11);
            }
        }
    }
}
```

#### Fake

Le Fake permet d'implémenter la classe comme on le souhaite.

Dans l'exemple ci-dessous, dans la classe "FakeTime", le fake permet de retourner une propriété qui sera ensuite modifié comme on le souhaite dans les tests (on pourra choisir la date que l'on souhaite).

```c#
namespace HelloworldTests
{
    public class FakeTime : ITime
    {
        //Créer une propriété qui sera retourné dans le getter de Date
        public DateTime DateToReturn { get; set; }

        public DateTime Date
        {
            get
            {
                return DateToReturn;
            }
        }
    }
}
```

#### Spy

Le Spy fonctionne comme un Stub mais en enregistrant les informations pendant le test que l'on pourra aller chercher ensuite.

Le Spy peut être très utile pour savoir combien de fois une méthode a été appelée ou savoir pourquoi le test échou.



#### Mock

Le Mock est un objet qui est une substitution complète de l'implémentation originale d'une classe concrète.

Le Mock a le même but que le Fake mais permet de ne plus écrire la classe qui remplace l'originale. Le mock utilise des librairies qui vont permettre de générer dynamiquement l'objet de doublure dans le corps du code de tests. 

Il existe 2 références de librairies : 
* NMock3 : simple mais malheureusement plus maintenu
* Moq : mêmes fonctionnalités mais avec une syntaxe moins évidente

Ces librairies s'ajoutent via les packages NuGet. 




#### Exemple avec un Fake  

*Exemple :* Avoir une fonction GetHelloMessage dans Message qui retourne un message selon l'heure et le jour. 

Le problème est que dans cette fonction, on initialise une date à la date actuelle. Cela empêche de pouvoir tester le code avec des tests unitaires. 

Solution :  

* Créer une interface pour isoler la dépendance : 
    * nom du fichier : ITime.cs dans le projet "Helloworld"
    * contient une propriété "Date" de type DateTime : 
    ```c#
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;

    namespace Helloworld
    {
        public interface ITime
        {
            DateTime Date { get; }
        }
    }
    ```
* Dans la classe Message :
    * ajouter un attribut du type de l'interface "ITime \_time"
    * Utiliser l'attribut dans la méthode 'GetHelloMessage' : \_time.Date.DayOfWeek pour la date du jour par exemple
```c#
namespace Helloworld
{
    public class Message
    {
        //Attributs déterminant les différentes tranches horaires
        protected int matin = 9;
        protected int midi = 13;
        protected int soir = 18;
        private ITime _time;

         public String GetHelloMessage()
        {
            //date = new DateTime(2018, 08, 20, 8, 52, 12);
            String message = "";
            //Pour la tranche vendredi soir au lundi matin
            if (date.DayOfWeek == DayOfWeek.Friday && date.Hour >= this.soir || date.DayOfWeek == DayOfWeek.Saturday || date.DayOfWeek == DayOfWeek.Sunday || date.DayOfWeek == DayOfWeek.Monday && date.Hour < this.matin)
            {
                message = "Bon week-end";
            }
            //...
        }
    }
}
```
* Créer une classe concrète pour impléter l'interface ITime permettant ainsi de donner la date actuelle :
    * nom fichier : Time.cs dans projet 'Helloworld'
    * Pour dire que la classe implémente une interface : 'public class MaClasse : MonInterface'
    * Implémenter "Date" en complémentant le getter : 
    ```c#
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;

    namespace Helloworld
    {
        public class Time : ITime
        {
            public DateTime Date
            {
                get
                {
                    return DateTime.Now;
                }
            }
        }
    }
    ```
* Dans la classe Message, ajouter dans le constructeur l'initialisation de l'attribut ITime \_time : 

**A ce niveau, nous avons isolé la dépendance et le code fonctionne correctement. Maintenant, pour réaliser les tests unitaires, il faut injecter les dépendances.**

* Dans la classe Message 
    * ajouter un constructeur contenant un paramètre supplémentaire qui sera la Date souhaitée de type ITime 
    * Initialiser l'attribut \_time avec le nouveau paramètre 
    * A la place de "public" mettre "internal" pour la visibilité du constructeur, cela empêchera le client d'utiliser ce constructeur réservé aux tests unitaires
    * Pour pouvoir utiliser ce nouveau constructeur, ajouter dans le fichier "AssemblyInfo.cs" (projet Helloworld), à la fin la ligne : 
    ```c#
    [assembly: InternalsVisibleTo("HelloworldTests")]
    ```
    * Nouveau constructeur dans la classe Message : 
    ```c#
    //Constructeur pour les tests unitaires 
    internal Message(ITime time, int matin, int midi, int soir)
    {
        this.matin = matin;
        this.midi = midi;
        this.soir = soir;
        _time = time;
    }
    ```
* Créer un Fake pour pouvoir implémenter l'interface ITime avec les données que l'on souhaite :
    * Créer dans le projet test "HelloworldTests" un dossier "Fakes" et ajouter une classe "FakeTime"
    * Cette classe FakeTime implémente l'interface ITime 
    * Ajouter une propriété avec une visibilité public "DateTime DateToReturn {get;set;}"
    * Implémenter Date (qui est dans l'interface) en complétant le getter avec un return de la propriété DateToReturn
    ```c#
    using Helloworld;
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;

    namespace HelloworldTests
    {
        public class FakeTime : ITime
        {
            public DateTime DateToReturn { get; set; }

            public DateTime Date
            {
                get
                {
                    return DateToReturn;
                }
            }
        }
    }
    ``` 

* Dans la classe Test "MessageTests.cs", créer un test pour chaque message que l'on souhaite tester. Dans un test : 
    * Créer une instance de FakeTime pour générer une date précise 
    * Attribuer à la propriété DateToReturn (de la classe FakeTime) la valeur de la date souhaitée
    * Instancier un objet Message (classe que l'on souhaite tester)
    * Stocker le résultat de la méthode que l'on test "GetHelloMessage" dans une variable
    * Comparer cette variable au résultat que l'on attend (message "bonjour" par exemple pour le matin en semaine)
    ```c#
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using Helloworld;
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using HelloworldTests;

    namespace Helloworld.Tests
    {
        [TestClass()]
        public class MessageTests
        {
            [TestMethod()]
            public void MessageTest()
            {
                //Retourner un échec du test
                //Assert.Fail();
            }

            //Tester que le message retourne "Bonjour" le matin
            [TestMethod()]
            public void GetHelloMessageTest_Bonjour()
            {
                //Créer une instance de FakeTime pour générer une date précise
                FakeTime fake = new FakeTime();
                fake.DateToReturn = new DateTime(2018, 08, 21, 9, 0, 0);
                //Créer une instance de l'objet Message avec la date que je souhaite
                Message message = new Message(fake, 9, 13, 18);
                //Stocker le résultat de l'appel à la méthode que je test
                String resultat = message.GetHelloMessage();
                //Je m'attends à avoir le résultat suivant 
                StringAssert.Contains(resultat, "Bonjour");
            }
        }
    }
    ```

**Refactor du constructeur de la classe Message** 
* Pour le constructeur classique étant utilisé pour le programme, indiquer qu'il utilise le constructeur pour les tests avec comme paramètre "date" une instance de la classe "Time" (classe générant la date actuelle)
* ":this" (à positionner avant les crochets) indique qu'on utilise l'autre constructeur
```c#
//Constructeur prenant en paramètres les différentes tranches horaires
public Message(int matin, int midi, int soir)
    :this (new Time(), matin, midi, soir)
{
}

//Constructeur pour les tests unitaires 
internal Message(ITime time, int matin, int midi, int soir)
{
    this.matin = matin;
    this.midi = midi;
    this.soir = soir;
    _time = time;
}
```


### Mini-Projet

Avoir une solution qui permet d'afficher un message selon l'heure et le jour avec une boucle tant que l'utilisateur ne tape pas "exit".

Code du "main" dans le fichier "Program.cs" :
```c# 
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Helloworld
{
    class Program
    {
        static void Main(string[] args)
        {
            String saisie = "";
            do
            {
                //Créer une instance de la classe message
                Message message = new Message(9, 12, 20);
                //Afficher la résultat de la méthode GetHelloMessage (retournant un message)
                System.Console.WriteLine(message.GetHelloMessage());

                //Poser une question à l'utilisateur 
                System.Console.WriteLine("Ecrire 'exit' pour terminer");
                //Récupérer l'entrée utilisateur 
                saisie = System.Console.ReadLine();
            } while (saisie != "exit");
            
        }
    }
}
```
