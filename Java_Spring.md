# Spring 


Ressources : 
* [Vidéos complètes JavaBrains](https://www.youtube.com/watch?v=9mFcT2f8JJI&list=PLmbC-xnvykcghOSOJ1ZF6ja3aOgZAgaMO&index=32)
* [Cours débutants](https://o7planning.org/fr/11267/le-tutoriel-de-spring-boot-pour-les-debutants#a5292734)


## Démarrer un projet Spring Boot 

Avec IntelliJ Idea, il est possible de créer un projet déjà paramètré 
* File / New / Project / Spring Initializr 
* Créer un package dans l'arborescence 'src/main/java'
* Créer la classe principale 
```java
package campus;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

//Déclarer qu'il s'agit d'une application Spring Boot
@SpringBootApplication

public class Jeu {

    public static void main(String[] args){
        
        //Méthode static magique qui fait tout, il y aura uniquement cette ligne
        SpringApplication.run(Jeu.class , args);

    }
}
```

* Créer une Classe qui sera un controller  
```java
package com.campus.testwebapp;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

//Indiquer qu'il s'agit d'un Controller respectant l'architecture Rest
@RestController
public class Hello {

	//Lorsque l'url "/hello" sera ouvert, la méthode qui suit sera exécutée
    
    @RequestMapping("/hello")
    public String sayHello(){
        return "Coin coin";
    }
}

```
* Pour tester : localhost:8080/hello

* Créer une nouvelle Classe qui sera également un Controller : la méthode retourne une liste de Topic
```java
package com.campus.testwebapp;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Arrays;
import java.util.List;

@RestController
public class TopicController {

    @RequestMapping("/topics")
    public List<Topic> getAllTopics(){
        return Arrays.asList(
                new Topic("spring", "spring Framework", "sprint Framework Description"),
                new Topic("java", "Core Java", "Core Java Description"),
                new Topic("javascript", "JavaScript", "Javascript Description")
        );
    }
}
```
* A noter, la Classe Topic a été créée également 
```java
package com.campus.testwebapp;

public class Topic {

    private String id;
    private String name;
    private String description;

    //getters et setters

	//Constructeur simple 
    public Topic() {

    }
    //Constructeur avec paramètres
    public Topic(String id, String name, String description) {
        this.id = id;
        this.name = name;
        this.description = description;
    }
}
```

## Spring Intializr

Outils disponible en ligne pour créer un projet Spring Boot en quelques clics. 

[Spring Initializr](https://start.spring.io/)

Permet de choisir les dépendences que l'on souhaite ajouter au projet : 
* web
* jpa
* devltools
* ...

Importer dans l'IDE en indiquant "import d'un projet maven déjà existant"

## Architecture d'un projet 

Architecture d'un projet Spring Boot 
* src/main/java : stocker les classes (controllers, services...)
* src/main/resources :
    * static : css, js .. fichier static
    * templates : templates
	* contient un fichier "application.properties" permet de changer les propriétés de notre projet Spring Boot
* src/main/test


*Exemple : changer le Port de notre projet*
* Dans le fichier "application.properties" : 
```java
server.port = 8081
```
Le site sera alors disponible sur "localhost:8081/.."

[Liste des propriétés disponibles modifiables](https://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html)


## RequestMapping("url")

Permet de gérer les routes du site.

* Syntaxe de base : @RequestMapping("/url")
```java
@RequestMapping("/topics")
//ici la méthode qui sera exécutée lors de l'ouverture de l'url
``` 

* Ajouter des éléments dynamiques dans les {} et préciser dans les paramètres de la méthode @PathVariable : 
```java
//Methode permettant de retourner un Topic en entrant l'url "topics/{id}"

@RequestMapping("/topics/{id}")
public Topic getTopic(@PathVariable String id) {
	return topicService.getTopic(id);
}
```

* @PathVariable peut avoir des paramètres : dans le cas précédent {id} et le paramètre avaient le même nom. Mais ce n'est pas le cas :
```java
//Methode permettant de retourner un Topic en entrant l'url "topics/{id}"

@RequestMapping("/topics/{foo}")
public Topic getTopic(@PathVariable("foo") String id) {
	return topicService.getTopic(id);
}
```

* Déclarer une méthode "POST" : @RequestMapping(method , value)
	* method : recherche dans la liste énumére "RequestMethod" la méthode POST 
	* value : indiquer l'url
```java
@RequestMapping(method = RequestMethod.POST, value = "/topics")

public void addTopic() {}
```





## Projet implémenter une API 

* Classe Topic avec attributs privés id, name, description (getters, setters) et constructeurs 
* Classe TopicController : il s'agit d'un Controller Rest 
* Classe TopicService : Traiter les données 

Classe Topic 
```java
package com.campus.testwebapp;

public class Topic {

    private String id;
    private String name;
    private String description;

	//getters et setters

	//Constructeur simple
    public Topic() {

    }

    //Constructeur avec paramètres 
    public Topic(String id, String name, String description) {
        this.id = id;
        this.name = name;
        this.description = description;
    }
}


```

Classe TopicService
```java
package com.campus.testwebapp;

import org.springframework.stereotype.Service;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

//Le service permettra de faire le lien avec la BDD
@Service
public class TopicService {

    //Attribut topics stockant dans une liste les topics
    private List<Topic> topics = new ArrayList<>(Arrays.asList(
            new Topic("spring", "spring Framework", "sprint Framework Description"),
            new Topic("java", "Core Java", "Core Java Description"),
            new Topic("javascript", "JavaScript", "Javascript Description")
    ));

    //Methode permettant de retourer tous les topics
    public List<Topic> getAllTopics() {
        return topics;
    }

    //Methode permettant de retourner un seul topic recherchant dans la liste de Topics au niveau de l'id
    public Topic getTopic(String id) {
        return topics.stream().filter(t -> t.getId().equals(id)).findFirst().get();
    }

    //Methode permettant d'ajouter un Topic à la liste
    public void addTopic(Topic topic) {
        topics.add(topic);
    }

    //Methode permettant de modifier un Topic
    public void updateTopic(String id, Topic topic) {
        for (int i = 0 ; i < topics.size() ; i++) {
            Topic t = topics.get(i);
            if (t.getId().equals(id)) {
                topics.set(i, topic);
                return;
            }
        }
    }

    //Methode permettant de supprimer un Topic
    public void deleteTopic(String id) {
        topics.removeIf(t -> t.getId().equals(id));
    }
}
```

Classe TopicController 
```java
package com.campus.testwebapp;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
public class TopicController {

    //Créer une instance du topicService
    @Autowired
    private TopicService topicService;

    //Méthode permettant d'afficher tous les topics sur l'url /topics
    @RequestMapping("/topics")
    public List<Topic> getAllTopics(){
        return topicService.getAllTopics();
    }

    //Methode permettant de retourner un Topic en entrant l'url "topics/{id}"
    @RequestMapping("/topics/{id}")
    public Topic getTopic(@PathVariable String id) {
        return topicService.getTopic(id);
    }

    //Methode POST permettant d'ajouter un Topic à la liste
    @RequestMapping(method = RequestMethod.POST, value = "/topics")
    public void addTopic(@RequestBody Topic topic) {
        topicService.addTopic(topic);
    }

    //Methode PUT permettant de modifier un Topic
    @RequestMapping(method = RequestMethod.PUT, value = "/topics/{id}")
    public void updateTopic(@RequestBody Topic topic, @PathVariable String id) {
        topicService.updateTopic(id, topic);
    }

    //Methode DELETE permettant de supprimer un Topic
    @RequestMapping(method = RequestMethod.DELETE, value = "/topics/{id}")
    public void deleteTopic(@PathVariable String id) {
        topicService.deleteTopic(id);
    }
}
```


## Se connecter à une BDD intégrée

JPA : Java Persistence API

* Créer un projet Spring Initializr avec les dépendences suivantes :
    * Web
    * JPA
    * Apache Derby : contient une BDD intégrée

* Indiquer dans la classe Topic (la ressource) qu'il s'agit d'une table de BDD et préciser la clé primaire 
```java
package projetJPA;

import javax.persistence.Entity;
import javax.persistence.Id;

//Entity permet de dire à JPA de créer une table Topic avec les champs correspondant aux attributs
@Entity
public class Topic {

    //@Id indique que l'attribut sera la clé primaire
    @Id
    private String id;
    private String name;
    private String description;

    //getters, setters, constructeurs
}
```
* Créer une interface "TopicRepository" qui extends de "CrudRepository" en indiquant <Ressource, Type id>
```java
package projetJPA;

import org.springframework.data.repository.CrudRepository;

//Interface extends de CrudRepository contenant toute la logique CRUD
public interface TopicRepository extends CrudRepository<Topic, String> {
    
}
```
* Le TopicController reste le même que précédemment 
* Créer dans le TopicService une instance de type TopicRepository et écrire les méthodes pour le CRUD
```java
package projetJPA;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

//Le service permettra de faire le lien avec la BDD
@Service
public class TopicService {

    //Instance de TopicRepository
    @Autowired
    private TopicRepository topicRepository;

    //TopicRepository a plusieurs méthodes intégrées permettant le CRUD

    //Methode permettant de retourner tous les topics
    public List<Topic> getAllTopics() {
        List<Topic> topics = new ArrayList<>();
        topicRepository.findAll()
                .forEach(topics::add);
        return topics;
    }

    //Methode permettant de retourner un seul topic recherchant dans la liste de Topics au niveau de l'id
    public Topic getTopic(String id) {
        return topicRepository.findById(id).get();
    }

    //Methode permettant d'ajouter un Topic à la liste
    public void addTopic(Topic topic) {
        topicRepository.save(topic);
    }

    //Methode permettant de modifier un Topic
    public void updateTopic(String id, Topic topic) {
        topicRepository.save(topic);
    }

    //Methode permettant de supprimer un Topic
    public void deleteTopic(String id) {
        topicRepository.delete(topicRepository.findById(id).get());
    }
}
```

Avec l'instance de type TopicRepository il y a plusieurs méthodes intégrées permettant le CRUD :

| Méthode | Objectif | 
|:-------:| ---------|
| findAll() | Retourner l'ensemble des éléments 
| findById(id).get() | Retourner un élément précis grâce à l'id
| save(ressource) | Créer ou Modifier un élément 
| delete(ressource) | Supprimer 


#### Créer des relations entres tables 

Un topic peut avoir plusieurs cours : relation one-to-many