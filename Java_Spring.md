# Spring 


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

