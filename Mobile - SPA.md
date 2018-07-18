
# Glossaire 

| Glossaire | Définition |
| :--------:| -------|
| Xcode | IDE pour le développement d'applications mobiles iOs avec les langages Objective C et Swift, permettant également de compiler le code source
| Objective-C | Langage compilé utilisé notamment pour le développement d'applications mobiles pour iOS
| Android Studio | IDE pour le développement d'applications mobiles Android avec le langage Java permettant également de compiler le code source
| Eclipse | IDE pour le développement d'applications mobiles Android avec le langage Java permettant également de compiler le code source
| Java | Langage compilé utilisé notamment pour le développement d'applications mobiles pour Android
| SDK (Software Development Kit) | Ensemble d'outils d'aide à la programmation pour concevoir des logiciels, jeux, applications mobiles pour un terminal et/ou un système d'exploitation spécifique. Le code est organisé sous forme de librairies permettant d'utiliser les fonctions natives du téléphone (GPS, bluetooth, appareil photo..) et proposant des éléments graphiques standards de l'OS. Ce code ne peut être intégré dans le code source, il faut mettre en place des "ponts" pour communiquer avec le SDK et appeler les fonctionnalités.   
| Cordova | Framework open-source pour le développement mobile permettant d'exploiter les technologies Web courantes (HTML, CSS et JavaScript) pour développer des applications multi-plateformes en évitant d'utiliser les langages natifs propres aux différentes plateformes. 
| PhoneGap | Framework open-source pour créer des applications mobiles avec des technologies web classiques (HTML, CSS, JavaScript) et de compiler le code pour la plateforme souhaitée (iOS, Android, Windows Phone) 	
| Vue.js | Framework open-source pour JavaScript intégrant des librairies
| React | Framework pour JavaScript permettant de manipuler le DOM
| Angular | Framework pour développer une application avec JavaScript 
| NPM | Gestionnaire de paquets officiel de Node.js, il gère notamment les dépendances pour une application
| Ionic | Framework open-source permettant de créer du code pour plusieurs plateformes
| Single Page App | Application web accessible via une page web unique en interaction avec les utilisations de l'utilisateur 
| App native | Application conçue spécifiquement pour un système d'exploitation (OS) avec un langage et une/des technologie(s) appropriés. Réalisée à partir de langage natif pur (Objective C pour iOS, Java sur Android, C# sur Windows Phone)
| App hybride | Le contenu web (HTML, CSS, JavaScript) est "encapsulé" dans une sur-couche applicative (technologies utilisables : Apache Cordova, PhoneGab...)
| WebApp | Application avec du contenu interactive et conçue comme un logiciel de bureau ou une application (ex : Google Drive). Peut être exécuté soit avec un navigateur web ou depuis un smartphone
| Compilateur | Programme permettant de transformer un code source écrit dans un langage de programmation en un autre langage pour qu'il puisse être exploité par une machine
| API  | (Application Programming Interface) Interface pour les applications permettant de faire communiquer 2 programmes logiciels
| RESTFUL | Désigne une API REST, c'est-à-dire qu'elle imite le fonctionnement du web dans les échanges entre un client et un serveur (requête et réponse). Les réponses du serveur peuvent être délivrées dans plusieurs formats (JSON, XML, CSV, RSS) mais JSON est souvent utilisé
| Stores : Play et itunes | Magasins d'applications permettant aux utilisateurs de télécharger des applications 
| Task runner | Application permettant d'automatiser les tâches régulières. 
| Dépendance | Un module a besoin d'un autre module pour fonctionner 
| JSON | JavaScript Object Notation, format de données permettant de représenter de l'information accompagnée d'étiquettes permettant d'en interpréter les divers éléments, sans aucune restriction sur le nombre de celles-ci 


Ressources : 
* [Développement d'une application mobile native](http://www.mobizel.com/2015/04/developpement-dune-application-mobile-native-13/)
* [C'est quoi un SDK](http://www.mobizel.com/2015/04/definition-cest-quoi-un-sdk/)
* [Différences Webapp, Application hybride, native](http://www.mobizel.com/2015/02/webapp-application-hybride-native-quelle-est-la-difference/)
* [Différences WebApp et Application Mobile](http://www.mobizel.com/2015/02/webapp-ou-application-mobile-quel-developpement-technique-pour-votre-projet-23/)
* [Cordova Apache](https://cordova.apache.org/docs/en/latest/guide/overview/)
* [Developper une application mobile](https://www.grafikart.fr/blog/developper-application-mobile)
* [Vue.js](https://www.grafikart.fr/formations/vuejs)
* [Gulp.js](https://www.grafikart.fr/tutoriels/html-css/gulp-js-490)
* [Frameworks JavaScript](https://www.grafikart.fr/tutoriels/javascript/frameworkjs-744)


# Technologies natives

## Application mobile native

**Application mobile native : Application conçue spécifiquement pour un système d'exploitation (OS) avec un langage et une/des technologie(s) appropriés.**

3 étapes de conception :
* Rédaction du code source : 
	* Langage de programmation spécifique pour chaque OS 
	* Communiquer avec le SDK native via le code source
* Compilation du code source (par l'IDE) : les logiciels fonctionnent avec du code binaire
* Génération du code binaire natif : le compilateur transforme le code source en code binaire et génère un fichier 

| Système d'exploitation | Langage | IDE 
| :---------------------:| :-------:| :-----:|
| iOS (Apple) | Objective C et Swift | Xcode
| Android | Java | Android Studio ou Eclipse
| Windows Phone | C# | Visual Studio

## SDK Cordova

Framework open-source pour le développement mobile. 

Il permet d'exploiter les technologies Web courantes (HTML, CSS et JavaScript) pour développer des applications multi-plateformes en évitant d'utiliser les langages natifs propres aux différentes plateformes. 



# Technologies hybrides 

## Application hybride 

Le contenu web (HTML, CSS, JavaScript) est "encapsulé" dans une sur-couche applicative (technologies utilisables : Apache Cordova, PhoneGap...), l'application est donc disponible pour plusieurs OS.

Une application mobile hybride est développée à partir de langages web (HTML5, JavaScript, CSS…). Cependant, elle s’appuie également sur des technologies natives mobiles pour utiliser certaines fonctionnalités du smartphone.

Bien que développée avec du web, il s’agit tout de même bien d’une « application » dans le sens ou elle sera téléchargée depuis les magasins d’applications et installée sur le mobile, contrairement à la web app qui n’est consultable que depuis un navigateur. 

Par exemple, LinkedIn est une application mobile hybride.

Il existe différentes technologies de développement d’application hybride : PhoneGap, Rho Mobile ou Apache Cordova.


## Outils : Gulp, NPM, Cordova, Ionic

### GULP

GULP est un task runner, c'est-à-dire qu'il automatise des tâches régulières (minifier ou concaténer du CSS ou du JavaScript, supprimer des fichiers...). 

GULP fonctionne avec Node.js. 

### NPM : Node Package Manager

NPM est le gestionnaire des packages et dépendances pour Node.js. 

### Cordova 

Framework open-source pour le développement mobile. 

Il permet d'exploiter les technologies Web courantes (HTML, CSS et JavaScript) pour développer des applications multi-plateformes en évitant d'utiliser les langages natifs propres aux différentes plateformes. 

### Ionic 

Ionic est un framework permettant notamment de développer des applications hybrides. 

Ce framework open source permet de développer une application déployable sur plusieurs environnements tel qu’un site web ou une application mobile pour des systèmes tel que Android ou iOS ou Windows Phone.

Ionic s’appuie sur AngularJS pour la partie application web du framework et sur Cordova pour la partie construction des applications natives.


## API RESTFUL 

Désigne une API REST, c'est-à-dire qu'elle imite le fonctionnement du web dans les échanges entre un client et un serveur (requête et réponse). 

Les réponses du serveur peuvent être délivrées dans plusieurs formats (JSON, XML, CSV, RSS) mais JSON est souvent utilisé.


# WebApp & Application mobile 

## WebApp 

C’est un logiciel applicatif hébergé sur un serveur et accessible depuis un navigateur Internet. Elle a une ergonomie et des fonctionnalités spécifiques adaptées aux contraintes des terminaux mobiles et ne peut pas fonctionner sans connexion Internet.

Son avantage est sa compatibilité multiplateforme. Hébergée sur un serveur, elle peut afficher son contenu sur plusieurs systèmes d’exploitation et plusieurs navigateurs. Il est également possible de concevoir une webapp responsive design pour la rendre compatible à toutes les tailles d’écran.

## Application Mobile 

C’est un logiciel développé spécifiquement pour un système d’exploitation mobile (iOS, Android, Blackberry, Windows Phone, etc.). Elle doit être téléchargée depuis un magasin d’applications mobiles (store) puis installée sur le périphérique. 

L’application mobile peut fonctionner hors-ligne et se baser sur les fonctionnalités natives du terminal (appareil photo, géolocalisation, etc.).




# Principe général 

Pour une application hybride tout se fait une seule page HTML (SPA). Les données échangées entre le client et le serveur sont dans le format JSON. 

L'échange entre le client et le serveur respecte l'architecture REST qui se base sur l'architecture du protocole HTTP. 

Pour créer la SPA, il est nécessaire d'utiliser un framework comme Vue.js qui fonctionnement comme un Framework et une librairie. 
Il permet d'avoir un routing et des composants (ensemble de HTML, JS et CSS). 

S'ajoute à cela, le gestionnaire de package NPM qui télécharge les librairies et automatise des tâches répétitives. 



# Single Page App (SPA)


## Définition

Single Page App ou Application monopage en français

Il s'agit d'une application web accessible via une page web unique. Le but est d'éviter le chargement d'une nouvelle page à chaque action demandée et de fluidifier l'expérience utilisateur. 

Les SPA utilisent AJAX qui permet de communiquer avec le back-end sans recharger la page 

## Différences entre une SPA et un site web classique 

La différence se situe dans leur structur et la relation entre le navigateur et le serveur. 

| | SPA | Site Web Classique 
| ------ | ------ | --------------
| Structure | Composée d'une seule page | Composé de plusieurs pages 
| Rôle navigateur | Le rôle du navigateur est + important car la quasi-totalité de la logique applicative y est déportée  | Le rôle du navigateur  
| Rôle serveur | Fournir les ressources de l'application et exposer les données | Contient la logique applicative, il fournit les pages à afficher et réagit aux actions de l'utilisateurs 


## Avantages & Inconvénients des SPA

| Avantages | Inconvénients 
| ------ | ------ |
| Le contenu est chargé en une seule fois | Le site est plus long à charger
| Scroller est moins compliqué et risqué que de cliquer | Le site contient énormément de JavaScript pour proposer une navigation locale
| La maintenance est plus simple | Les utilisateurs peuvent être désorientés


Le navigateur effectue la majeure partie des tâches lourdes, ce qui signifie que les performances peuvent poser problème, en particulier sur les appareils mobiles moins performants.

Une réflexion approfondie doit être mise sur l'optimisation des moteurs de recherche (SEO) afin que votre site puisse être découvert par les moteurs de recherche et les sites de médias sociaux qui fournissent un aperçu des liens.


## Exemple 

Gmail est un exemple de SPA

http://www.opentuto.com/single-page-application/

https://en.wikipedia.org/wiki/Single-page_application


## Frameworks

Il existe de nombreux frameworks JavaScript qui facilitent la création de SPA, tels que:
* Angular
* React
* Ember 
* Meteor 
* Vue.js 




# Installation de l'environnement de développement

## Installer Android Studio 

* Télécharger Android Studio : [Lien téléchargement](https://developer.android.com/studio/index.html)
* Aide à l'installation : [Lien aide](https://developer.android.com/studio/install.html)


## Installer Node.js

* Télécharger Node.js : [Lien téléchargement](https://nodejs.org/fr/)


## Installer Cordova 

Infos installation : [Infos](http://cordova.apache.org/docs/en/latest/guide/platforms/android/index.html)

### Installer JDK (Java Development Kit)

* Télécharger la V161 : [Lien téléchargement](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

### Installer Cordova 

* Ouvrir un Bash, vérifier la présence de Node.js
```
node -v
```

* Installer Cordova :
```
npm install -g cordova
```

* Changer le PATH 
	* Windows + Pause 
	* Paramètres système avancés
	* Variables d'environnement
	* PATH
	* Récupérer le chemin de NPM : C:\Users\marion.chapuis\AppData\Roaming\npm
	* Nouveau : copier le chemin
	* Déplacer vers le haut dans la liste


# Projet Application

Informations sur la création d'un projet : [Lien infos](http://cordova.apache.org/#getstarted)

## Créer un projet 

Ligne de commande permettant de créer le dossier complet pour l'App : 
```
cordova create NomApplication
```


## Ajouter une plateforme

Pour connaître toutes les plateformes, se positionner dans le dossier puis : 
```
cordova platform
```

Ajouter une plateforme web : 
```
cordova platform add browser 
```

## Faire tourner l'application

Ligne de commande : 
```
cordova run NomPlateforme
```

Le projet est en ligne sur : localhost:8000
Le projet est compilé.

## Emuler Android 

Pour que notre ordinateur puisse fonctionner comme un Android, il faut émuler un Android 

* Redémarrer l'ordinateur et pendant le redémarrage appuyer 2 ou 3 fois sur "Echap"
* Dans le menu qui s'ouvre aller dans BIOS SetUp en cliquant ou appuyer sur F10
* Aller dans l'onglet "Advanced"
* Choisir "Systems Options"
* Cocher les  cases "Virtualization"
* Save (puis confirmer l'enregistrement)

## Faire tourner l'application sur la plateforme Android

### Sélectionner la bonne plateforme

Si la commande "cordova run android" donne une erreur et indique qu'il n'y a pas le "plateforme 26", cela peut se régler dans Android Studio

* Ouvrir dans Android Studio : Configure / Settings / System Settings / Android SDK
* Cocher la plateforme 26 (colonne "API Level") et appliquer 

### Tout fonctionne ?

Dans Android Studio, l'onglet "Tools" il doit y avoir "Android"

Paramétrer ensuite le téléphone souhaité pour la visualisation :
* Dans Android Studio, onglet "Tools"
* Android
* AVD Manager 

### Personnaliser les infos 

**Changer le nom de l'application** 
* Dans le Config.xml, modifier le "name"
```
<?xml version='1.0' encoding='utf-8'?>
<widget id="io.cordova.hellocordova" version="1.0.0" xmlns="http://www.w3.org/ns/widgets" xmlns:cdv="http://cordova.apache.org/ns/1.0">
    <name>Marion</name> // Nom de l'application
    <description>
        A sample Apache Cordova application that responds to the deviceready event.
    </description>
    <author email="dev@cordova.apache.org" href="http://cordova.io">
        Apache Cordova Team
    </author>
    <content src="index.html" />
    <plugin name="cordova-plugin-whitelist" spec="1" />
    <access origin="*" />
    <allow-intent href="http://*/*" />
    <allow-intent href="https://*/*" />
    <allow-intent href="tel:*" />
    <allow-intent href="sms:*" />
    <allow-intent href="mailto:*" />
    <allow-intent href="geo:*" />
    <platform name="android">
        <allow-intent href="market:*" />
    </platform>
    <platform name="ios">
        <allow-intent href="itms:*" />
        <allow-intent href="itms-apps:*" />
    </platform>
    <engine name="browser" spec="^5.0.3" />
    <engine name="android" spec="^7.0.0" />
</widget>

```


# Mémo Cordova 

## Commandes Cordova

| Commande | Explication 
| :-------:| ---------|
| cordova create NomApplication | Créer un nouveau projet (création de l'intégralité du dossier)
| cordova platform add NomPlateforme | Générer l'application pour une plateforme donnée pour le projet (plusieurs plateformes peuvent être créées)
| cordova platform | Liste des plateformes 
| cordova run NomPlateforme | Lancer l'application sur la plateforme souhaitée et compiler le contenu
| cordova plugin add NomPlugin | Ajouter un plugin

## Structure d'un projet Cordova 

| Répertoire | Contenu
| :-------:| ---------|
| platforms | Contient les projets générés pour les différentes plateformes au projet
| plugins | Contient les différents plugins installés pour le projet 
| www | Contient les fichiers de développement (index.html, css, img, js)
| package.json | Récapitulatif des dépendances (plugins, packages, librairies) installées pour le projet par NPM (fichier propre à Node.js)
| config.xml | Fichier de configuration de Cordova, reprend le nom du projet, les infos sur l'auteur, lien vers le fichier index.html, infos sur l'application, les plateformes, "content" : accès à toutes les fonctionnalités du support... (fichier propre à Cordova)
| www/index.html | Source qui sera ensuite générée pour chaque plateforme



# IDE 

WebStorm : IDE pour JavaScript de JetBrains

Importer des librairies : File / Settings / Languages & Frameworks / Javascript / Librairies puis "download" (ex : jquery, bootstrap)


# Vue.js 

Ressources : 
* Github Librairies, bonnes pratiques : [Lien Github](https://github.com/vuejs/awesome-vue)

## Mémo Cordova + Vue.js 

| Répertoire | Contenu
| :-------:| ---------|
| build | 
| config |
| node_modules |
| resources |
| src |
| static |
| www | 


| Commande | Utilisation 
| :-------:| ---------|
| npm run dev | 
| npm run build | 


## Utilisation Vue.js 

### Charger la librairie Vue.js avec un CDN & Vue DevTools

Ajouter dans les liens (comme par exemple : Bootstrap, jQuery..), la liaison avec la librairie Vue.js :
```
<script src="https://cdn.jsdelivr.net/npm/vue"></script> // Vue.js
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.13/dist/vue.js"></script> //Vue DevTools
```

#### Récupérer un texte entré dans un champ saisie 

```
<div id="app">
    <label for="titre">Titre : </label>
    <input type="text" id="titre" v-model="titre"/>
    <h1>{{titre }}</h1>
</div>

<script>
    var app = new Vue({
        el : '#app',
        data :{
            titre : ''
        }
    })
</script>
```


#### Récupérer un texte entré lors d'un évènement 

Lorsque je clique sur un bouton, le titre prend la valeur de mon input

```
<div id="app">
    <label for="titreh2" autofocus>Mon petit titre : </label>
    <input type="text" id="titreh2" v-model="titreh2"/>
    <button v-on:click="affiche">Ajouter un titre</button>  // alternative : v-on:click="titreAffiche = titreh2"
    <h2>{{titreAffiche }}</h2>
</div>

<script>
    var app = new Vue({
        el: '#app',
        data: {
            titreh2: '',
            titreAffiche: ''
        },
        methods: {
            affiche: function () {
                this.titreAffiche = this.titreh2 
            }
        }
    })

</script>
```


#### Changer des classes 

Lorsque je coche ma checkbox, les titres sont en rouge (class "red" dans style.css mettant en rouge)

```
<h2 :class="{red : isRed}">{{titreAffiche }}</h2> // la classe "red" est appliquée si "isRed" est "true"
// :class et v-bind:class sont 2 syntaxes identiques

<input type="checkbox" v-model="isRed">Je vois Rouge</input> // v-model me permet de récupérer la valeur de mon input
```

#### Apparaître - disparaître 

2 possibilités pour afficher ou cacher un élément : 
* v-if : lorsque l'élément n'est pas affiché, il n'est pas présent dans le code 
* v-show : à l'inverse, même lorsqu'il est caché l'élément est présent dans le code

```html
<input type="checkbox" v-model="show">Magie Magie !</input>

<img v-if="show" id="crashounet" src="crash.png"/> // Si show = true alors l'image s'affiche
<img v-show="show" id="crashounet" src="crash.png"/> 
```


#### Boucle v-for
boucle : rajouter des clés

[documentation officielle](https://fr.vuejs.org/v2/guide/list.html)


```javascript
<template>
    <div>
        <h1>Liste des machines</h1>
        <machine v-for="machine in machines" :key="machine.id" :name="machine.name" :status="machine.status" :checked-at="machine.checkedAt"></machine>
    </div>
</template>

<script>
    import Machine from './Machine.vue';

    export default {
        components: {Machine},
        name: "machine-list",
        data() {
            return {
                machines: [{
                    id: 1,
                    name: 'What else ?',
                    status: true,
                    checkedAt: new Date(),
                }, {
                    id: 2,
                    name: 'Broken',
                    status: false,
                    checkedAt: new Date(),
                }]
            }
        }
    }
</script>
```

**Important : key**
Une boucle v-for demande la présence d'une clé (id), il faut donc préciser lorsqu'on fait la boucle qu'il existe un 'id' servant de 'key'
```javasript
<machine v-for="machine in machines" :key="machine.id">
```



## Mettre en place un projet buildé avec "vue-cli"

* Installer Vue-cli 
```bash
# install vue-cli
    $ npm install --global vue-cli
# create a new project using the "webpack" template
    $ vue init webpack-simple NomDuProjet
# install dependencies and go!
    $ cd my-project
    $ npm install
    $ npm run dev
```

* Webpack-simple : est un template de Vue.js

* Réponses aux questions lors du "vue init webpack"
    * nom du projet
    * description
    * auteur 
    * Licence MIT : appuyer sur entrée ou renseigner MIT
    * Use sass ? yes 

### Webpack 

Webpack permet de morceler le code sous forme de modules qui seront ensuite fusionnés en un seul fichier par Webpack.


## Ajouter un composant externe avec NPM : toggle button 

Ressources : [Lien Github](https://github.com/euvl/vue-js-toggle-button)

* Installer le composant en ligne de commande dans le projet 
```bash
npm install vue-js-toggle-button --save
```

* Importer dans le fichier "main.js" le composant 
```javascript
import ToggleButton from 'vue-js-toggle-button'
Vue.use(ToggleButton)
```

* Dans le html 
```html 
<toggle-button @change="onChangeEventHandler"/>

<toggle-button v-model="myDataVariable"/>

<toggle-button :value="false" 
               color="#82C7EB" 
               :sync="true" 
               :labels="true"/>

<toggle-button :value="true" 
               :labels="{checked: 'Foo', unchecked: 'Bar'}"/>
``` 

## Créer un composant 

Un composant est un élément personnalisable. Un peu comme une fonction pour du HTML.

Le composant est composé de :
* 'props' : données 
* 'template' : html 


**Exemple : composant 'test' affichant un titre H2**

* Créer le composant dans le fichier "main.js"
```javascript
Vue.component('test', {
  props: ['message'],
  template : `<h2>{{message}}</h2>`
});
```


```javascript
Vue.component('test', {
  props: ['message'],
  template : `<h2>{{message}}</h2>`
});

Vue.component('machine', {
  props: ['nom', 'active'],
  template : `<li :class="{red : !active}">{{nom}}<toggle-button :labels="{checked: 'on', unchecked:'off'}" v-model="active"/></li>`
});
```

```html
<test message="Liste des machines"></test>

<ul>
   <machine v-bind:nom="machine.name" v-bind:active="machine.status" v-for="machine in machines"></machine>
</ul>
```


## Créer un composant dans un autre fichier

En Vue.js tout est composant, pour faire un nouvel écran il nous faut un nouveau composant. 

Avec WebStorm : 
* Créer un nouveau fichier dans "src" en allant sur "File/New/Vue Component"
* Donner un nom de fichier "monfichier" sans l'extension ".vue"

Le composant "MachineList.vue" a la structure suivante :
```javascript
<template> // Mettre les élément dans une <div>
    <div>
        <h1>Mon titre</h1>
    </div>
</template>

<script>
    export default {
        name: "machine-list" //nom de la balise qui permettra d'appeler le composant
    }
</script>

<style scoped>
    div{
        background-color: aqua; //scoped permet d'appliquer le style uniquement au composant sans impacter le reste
    }

</style>
```

Dans le fichier "app.vue" afficher le composant :
* afficher le composant dans la div "app"
```javascript
<template>
    <div id="app">
        <machine-list></machine-list> //le composant est affiché
    </div>
</template>
```
* Importer le composant dans le script 
```javascript
<script>
    import MachineList from "./MachineList.vue"; //importer le composant 
```
* Déclarer le compsant 
```javascript
export default {
        components: {MachineList}, //déclarer le composant 
}
```

*A noter, dans WebStorm, il suffit simplement d'afficher le composant avec les balises et les importations et déclarations se font automatiquement **mais il faut ajouter '.vue' dans l'importation du composant***

* Vue globale du fichier 'app.vue'
```javascript
<template>
    <div id="app">
        <machine-list></machine-list> //le composant est affiché
    </div>
</template>

<script>
    import MachineList from "./MachineList.vue"; //importer le composant 

    export default {
        components: {MachineList, Machine}, //déclarer le composant 
        name: 'app',
        data() {
            return {
                msg: 'Welcome to Your Vue.js App',
            }
        },
        methods: {
            onMachinesListClick : function(){
                alert("consulter la liste des machines"); //afficher un message lorsqu'on click sur le bouton "liste machines"
            },
            onMapClick : function(){
                alert("consulter la carte"); //afficher un message lorsqu'on click sur le bouton "carte"
            }
        }
    }
</script>
```

### Passer des données : props

**Exemple**

Fichier du composant "Machine.vue" :

```
<template>
    <div>
        <h1>{{name}}</h1>
        <h3 v-if="status" class="green">Status {{msgMachineOk}}</h3>
        <h3 v-if="!status" class="red">Status {{msgMachineKo}}</h3>
        <h5>Dernière vérification : {{formatDate(checkedAt)}}</h5>
    </div>

</template>

<script>
    export default {
        name: "machine",
        props: ['name', 'status', "checkedAt"], //Je déclare mes props
        data() {
            return {
                msgMachineKo : 'KO',
                msgMachineOk : "OK",
            }
        },
        methods: {
            formatDate : function(dateBrute){
                return dateBrute.toLocaleString('fr-FR', {timeZone: 'UTC'});
            }
        }
    }
</script>
```

* Les props sont déclarées dans 'export default'
* Je place dans mon template les props 
```javascript
<h1>{{name}}</h1>
<h3 v-if="status"></h3>
``` 


Utilisation du composant dans un autre composant "MachineList.vue":

```
<template>
    <div>
        <h1>Liste des machines</h1>
        <!--<machine name="mamachine" status="true" checkedAt="12/03/2018"></machine>-->
        <machine :name="machine.name" :status="machine.status" :checked-at="machine.checkedAt"></machine>
    </div>
</template>

<script>
    import Machine from './Machine.vue';

    export default {
        components: {Machine},
        name: "machine-list",
        data() {
            return {
                machine: {
                    id: 1,
                    name: 'What else ?',
                    status: true,
                    checkedAt: new Date(),
                }
            }
        }
    }
</script>
```

* Pour passer des données dans un attribut, il faut ajouter ':' devant l'attribut : ':name="machine.name' (idem que v-bind:name="machine.name")

# Hook 

Evènements : 
create()
mounted()
beforeCreate()

# Propriétés calculées 

Les propriétés calculées ... 


**Exemple : afficher les machines selon le status 'ko', 'ok' et 'all'**

```javascript
<template>
  <div>
    <h1>Liste des machines</h1>
    <!--Bouton pour afficher les machines ok-->
    <button class="btn btn-lg btn-success" @click="afficheMachinesOk">Machines ok</button>

    <!--Bouton pour afficher les machines ko-->
    <button class="btn btn-lg btn-danger" @click="afficheMachinesKo">Machines ko</button>

    <!--Bouton pour afficher toutes les machines -->
    <button class="btn btn-lg btn-primary" @click="afficheMachineAll">Machines</button>

    <br><br>
    <!--Afficher la liste des machines selon leur status-->
    <machine v-for="machine in machineFilter" :key="machine.id" :machine="machine"></machine>

  </div>
</template>

<script>
  import Machine from './Machine.vue';

  export default {
    components: {Machine},
    name: "machine-list",
    props: ['machines', 'loading', 'error'],
    data() {
      return {
        statusMachine:'', //variable pour afficher les machines selon leur status
      }
    },
    methods: {
      afficheMachinesOk : function(){
        this.statusMachine = "true"; //statusMachine permet après de filtrer les machines avec un status "true"
      },
      afficheMachinesKo : function(){
        this.statusMachine = "false"; //statusMachine permet après de filtrer les machines avec un status "false"
      },
      afficheMachineAll : function(){
        this.statusMachine =  ''; //statusMachine étant null je pourrais afficher toutes les machines
      }
    },
    //computed: propriétés calculées
    computed:{
      machineFilter: function(){
        if(this.statusMachine === ''){
          return this.machines;
        }
        return this.machines.filter(machine => machine.status === this.statusMachine);
      }
    }
  }
</script>
```

**Explications**
* 3 boutons appelant des fonctions pour donner à la variable 'statusMachine' des valeurs différentes ("true", "false", "")
* 3 méthodes changeant la valeur de la variable 'statusMachine'
* 1 fonction 'machineFilter' qui si la variable 'statusMachine' est vide elle retourne toute la liste des machines sinon on applique une méthode 'filter' qui affichera les machines selon la valeur de leur status


# Mise en place d'un routeur

Le problème est que nous ne voulons pas avoir une seule page sur notre application. Nous devons avoir la possibilité de naviguer d'une page à l'autre, sans recharger la page ou sans afficher une nouvelle page html, nous avons besoin de mettre en place un routeur.

C'est la même chose que Laravel, sauf qu'ici le routeur est côté client, nous devons définir nos routes côté client et avoir moyen d'en changer.

Cela tombe bien, Vue a un routeur tout prêt que nous allons utiliser, [vue-router](https://router.vuejs.org/fr/installation.html)

## Installation 

2 possibilités pour installer le router :
* npm
* cdn

#### Installation avec NPM

* Avec npm, lancer la commande :
```bash
npm install vue-router
```

* Dans le fichier "main.js", importer VueRouter 
```javascript
import VueRouter from 'vue-router'
Vue.use(VueRouter) // a mettre avant (new Vue)
```

#### Téléchargement direct CDN

Unpkg.com fournit des liens CDN basés sur npm. Le lien ci-dessus pointera toujours vers la dernière version sur npm.
Incluez vue-router après Vue et l'installation sera automatique :

```javascript
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
```


## Utilisation du routeur 

Lien vers un exemple : [exemple](https://jsfiddle.net/yyx990803/xgrjzsup/)

#### Dans le fichier "main.js" : 

* Importer les composants 
```javascript
import MachineList from './MachineList.vue'
import MachinesMap from './MachinesMap.vue'
```
* Créer le tableau des routes 
```javascript
const routes = [
    {
        path: '/machines',
        component: MachineList
    },
    {
        path: '/map',
        component: MachinesMap
    },
]
```
* Créer une instance de route avec pour option "routes"
```javascript
const router = new VueRouter({
    routes
})
```
* Ajouter l'instance 'router' dans l'élément 'app' 
```javascript
new Vue({
    el: '#app',
    router, //ajouter l'instance router dans la Vue
    render: h => h(App)
})
```

#### Dans le fichier "app.vue"

* Appeler la route : balise 'router-link' et attribut 'to="/route"'
```javascript
<router-link to="/machines"  class="btn btn-lg btn-success">Consulter la liste des machines</router-link>
<router-link to="/map" class="btn btn-lg btn-success">Voir la carte</router-link>
```
* Ajouter la balise, une seule fois pour toutes les routes, en dessous des routes 
```javascript 
<router-view></router-view>
```


# Google Map


## Installer Google Map 

* Lancer la commande :
```bash
npm install vue2-google-maps
```

Documentation GitHub : [vue-google-maps](https://github.com/xkjyeah/vue-google-maps)

* Dans le fichier "main.js" :
```javascript
import * as VueGoogleMaps from 'vue2-google-maps'
Vue.use(VueGoogleMaps, {
  load: {
    key: 'Notre_Cle_API', //à récupérer sur Google
  }
})
```

* Récupérer une clé API google Map : [En cliquant sur 'Obtenir une clé'](https://developers.google.com/maps/documentation/javascript/get-api-key?refresh=1)

### Protéger la clé API 

* Mettre la clé API dans une variable, dans un fichier JavaScript qui ne sera pas commité :
```javascript
//Dans le fichier 'secret.js'
myKey = 'xxxxxxxxxxxxxxxxxxxxx'
```
* Dans le fichier 'main.js', appeler le fichier (require) et remplacer notre clé API dans 'Vue.use' par la variable :
```javascript
require('./secret.js') //appel au fichier js contenant la clé

import * as VueGoogleMaps from 'vue2-google-maps'
Vue.use(VueGoogleMaps, {
  load: {
    key: myKey
  }
})
```
* Créer un fichier 'x.example.js' pour permettre à d'autres collaborateurs de comprendre ce qu'est 'myKey' :
```javascript
myKey = 'Ma clé API Google' //Générer depuis Google API - obtenir une clé
```
* Ajouter dans le fichier '.gitignore', le fichier contenant la Clé à protéger :
```javascript
secret.js
```


## Afficher une Map

* Dans le template dans le fichier '.vue' :
```
<gmap-map
      class="maps"
      :center="{lat:45.1885, lng:5.7245}"
      :zoom="14"
    >
</gmap-map>
```

* Dans les balises 'style'
```
<style scoped>
.maps{
  width: 90%;
  height: 800px;
  margin: auto;
}
</style>
```

## Afficher des marqueurs 

* Dans le template du fichier .vue, ajouter les balises gmap-marker et une boucle v-for (car il y a plusieurs positions): 
```
<gmap-marker
    :key="machine.id"
    v-for="machine in machines"
    :position="machine.position" // position doit être un objet de la forme {lat: xxxx, lng: xxxx}
    :clickable="true" // permet de cliquer sur la position
    :draggable="true" //permet de bouger le marqueur
></gmap-marker>
```


## Initialiser la map sur la géolocalisation du navigateur

Afficher la map en centrant sur la position de l'utilisateur 

```javascript
<template>
    <gmap-map
      class="maps"
      v-show="!loading && !error.length"
      :center="{lat:maPosition.latitude, lng:maPosition.longitude}" //centrer sur la position de l'utilisateur
      :zoom="7"
    ></gmap-map>
</template

<script>
  import Machine from './Machine.vue';

  export default {
    name: "machines-map",
    components: {Machine},
    props: ['machines', 'loading', 'error'],
    data() {
      return {
        infoMachine: '', //Variable pour stocker les infos de la machine sur laquelle l'utilisateur a cliquée
        maPosition: {
          latitude: 48,
          longitude: 2,
        },
      }
    },
    methods: {
      affiche: function (objetMachine) {
        this.infoMachine = objetMachine; //récupérer les infos de la machine
      },
    },
    mounted() {
      if (navigator.geolocation) {
        let self = this;
        navigator.geolocation.getCurrentPosition(function (position) {
          self.maPosition = position.coords;
        })
      }
    }
  }
</script>
```

* mounted() : lance le script lorsque l'objet a été créé et que le composant est rattaché au DOM 
* let self = this : 'this' permet de remonter au parent, sauf que 'self.maPosition', le parent est celui qui appelle la 'fonction (position)'

# API 

## Consulter la documentation de l'API : exemple
* URL permettant de récupérer les 5 premières machines triées par nom
```
https://machine-api-campus.herokuapp.com/api/machines?limit=5&&sort=name
```
* adresse de l'API : 
```
https://machine-api-campus.herokuapp.com/
```
* afficher l'ensemble des machines 
```
api/machines
```
* limiter et trier 
```
?limit=5&&sort=name
```

## Installer la librairie AXIOS 

VueJS préconise l'utilisation de la librairie [axios](https://github.com/axios/axios) 

* Installer avec NPM axios
```bash
npm install axios
```
* Importer axios pour l'utiliser 
```javascript
<script>
  import axios from 'axios';
```

## Récupérer des données d'une API 

```javascript
<script>
  import axios from 'axios';

  export default {
    name: "machine-list",
    data() {
      return {
        machines: [],
        loading: false,
        error: null,
      }
    },
    created(){
      axios.get('https://machine-api-campus.herokuapp.com/api/machines').then(response =>{
      this.machines = response.data}) //j'ajoute dans mon tableau machines les données récupérées de l'API
      .catch(e => {
        this.errors.push(e) //ajoute dans 'error' les erreurs rencontrées
      })
    }
  }
</script>
```

## Paramétrer un message d'attente & d'erreur

* Partie Script
```javascript
<script>
  import Machine from './Machine.vue';
  import axios from 'axios';

  export default {
    components: {Machine},
    name: "machine-list",
    data() {
      return {
        machines: [], //la liste des machines est vide avant de télécharger les données de l'API
        loading: true, // loading est par défaut "true" pour afficher un message d'attente pendant le téléchargement
        error: [], //la liste des erreurs est vide et se remplira en cas d'erreurs de téléchargement
      }
    },
    created() {
      axios.get('https://machine-api-campus.herokuapp.com/api/machines').then(response => {
        this.machines = response.data; // les données récupérer s'ajoute dans la collection "machines"
        this.loading = false; //loading devient false afin de ne plus afficher le message d'attente
      })
        .catch(e => {
          this.loading= false; //ne plus afficher le message d'attente
          this.error.push(e); //ajouter les erreurs dans le tableau 'error'
        })
    },
  }
</script>
```

* Partie Template 
```html
<template>
  <div>
    <h1>Liste des machines</h1>

    <!--Afficher le message d'erreur s'il y a des erreurs-->
    <h2 class="erreur" v-if="error && error.length">Erreur téléchargement</h2>

    <!--Animation téléchargement avant l'arrivée des données API-->
    <h2 v-show="loading" class="msgLoading">Loading<br><i class="fa fa-circle-o-notch fa-spin fa-5x"></i></h2>

    <!--Afficher la liste des machines-->
    <machine v-for="machine in machines" :key="machine.id" :name="machine.name" :status="machine.status" :checked-at="machine.checkedAt"></machine>

  </div>
</template>
```

* Dans l'index HTML, ajouter le lien pour afficher les animations [fontawesome](https://fontawesome.com/)
```html
<head>
   <meta charset="utf-8">
   <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
   <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
   <script defer src="https://use.fontawesome.com/releases/v5.0.8/js/all.js"></script>
   <title>appli_parc_machines</title>
</head>
```

## Récupérer les données d'une API dans App.vue 

Pour pouvoir alimenter plusieurs composants avec une API, il faut l'appeler dans 'App.vue' : 
* Ajouter les props dans les composants 
```javascript
props: ['machines', 'loading', 'error'],
```
* Dans 'App.vue', ajouter dans Data les variables 'machines', 'loading', 'error'
```javascript 
data() {
      return {
        msg: 'Welcome to Your Vue.js App',
        machines: [],
        loading: true,
        error: [],
      }
    },
    created() {
      axios.get('https://machine-api-campus.herokuapp.com/api/machines').then(response => {
        this.machines = response.data; //ajouter dans la collection 'machines' les données de l'API
        this.loading = false; //désactiver le message d'attente de téléchargement
      })
        .catch(e => {
          this.loading = false; //désactiver le message d'attente de téléchargement
          this.error.push(e); //ajouter les erreurs rencontrées dans le tableau des erreurs
        })
    }
```
* Passer les données à 'App.vue' 
```
<router-view v-bind:machines="machines" :loading="loading" :error="error"></router-view>
```

## Importer des fichiers JavaScript

Pour construire une application dans l'esprit MVC, il est possible de créer des modèles.

Créer un répertoire "Models", par exemple, et mettre les fichiers JavaScript correspondant à nos modèles.

Exemple pour le jeu Bataille Navale, le répertoire contient :
* bateau.js
* caseBateau.js
* plateau.js
* casePlateau.js

#### Exporter les variables JS :

Les fichiers JS contiennent des variables, des fonctions, console.log et tout ce qu'il peut y avoir en JS. 

Pour pouvoir exporter ces informations : 
* Déclarer un "export default"
* Donner un nom au fichier pour l'export
* Ajouter les variables que l'on veut exporter

Par exemple, fichier bateau.js :
```JavaScript 
console.log("Bateau");

var objetBateau = {
  id : "id",
  nom : "nom bateau",
  taille : "nombre cases",
  cases : ["case", "case"],
  status : "true of false",
}

var idBateau = objetBateau.id;

export default {
  name : "bateau",
  idBateau,
  objetBateau
}
```

#### Importer dans un composant 

Pour importer ces informations dans un composant : 
* Créer un import du fichier
* Passer les variables JS dans la Data() 
* Pour appeler une variable JS utiliser le nom (donné dans export default - name) avec un point et le nom de la variable : monFichier.maVariable

Par exemple, composant App.vue :
```javascript
<template>
  <div id="app">
    <router-view/>
    <liste-bateaux></liste-bateaux> //mon composant "ListeBateaux"

    //Bouton avec onclick l'appel à une fonction
    <button class="btn btn-primary" v-on:click="afficherBateau(sousMarin)">afficher</button>

    //Afficher une variable de Data 
    {{sousMarin}}

  </div>
</template>

<script>
  import ListeBateaux from "./components/ListeBateaux.vue";
  //Importer mon fichier javascript en utilisant le nom donné dans "export default - name"
  import bateau from "./models/bateau.js";

  export default {
    components: {ListeBateaux},
    name: 'App',
    data() {
      return {
        sousMarin : bateau.objetBateau,
        afficherBateau : function (typeBateau) {
          console.log(typeBateau);
        }
      }
    }
  }
</script>
```


## Créer des composants avec VGC

[Lien NPM](https://www.npmjs.com/package/vue-generate-component)

VGC est une dépendance permettant de générer des composants en ligne de commande. 

* Installer VGC en global sur son ordinateur 
```bash
npm install -g vue-generate-component
``` 

* Créer un composant au format "Dossier comprenant les fichiers du composant " : 
```bash
vgc NomComposant
```
* Créer un composant au format "Dossier comprenant le composant en un seul fichier" :
```bash
vgc -s NomComposant --folder
```
* Créer un composant au format "Simplement le composant dans un fichier unique"
```bash
vgc -s NomComposant
```

