# TESTS FONCTIONNELS 

## Parcours clients 

Les tests fonctionnels pour les parcours clients les plus importants : 
* Créer un compte utilisateur
* Se connecter utilisateur 
* Générer un url simplifié avec un compte utilisateur
* Consulter les statistiques des url générés


## Cahier des tests fonctionnels 

* S'adresser à une personne qui ne connait pas du tout l'application 
* S'il y a des connexions, donner toutes les données à utiliser (ex : login, password...)


## Réaliser les tests avec Jest et Puppeteer 

Jest et Puppeteer permettent d'automatiser les tests.

Jest permet de faire les tests et Puppeteer permet de générer une connexion sur Chrome pour effectuer les tests de navigation.

### Lancer les tests 

Cloner le projet sur Github : 
```
git clone git@github.com:MarionChapuis/module-test-puppeteer.git
```

Installer les packages : 
```bash
npm install
```

Lancer l'ensemble des tests : 
```bash
npm test
```

Lancer les tests un par un (de façon séquencielle) : 
```bash
npm test -- --runInBand
```
**Attention** avec runInBand, les tests sont lancés l'un à la suite de l'autre mais dans le même process. 

S'il y a des connexions à un compte sur la fin d'un test, le test suivant commencera avec la session du compte du test précédent. Penser à bien effectuer les déconnexions des comptes utilisateurs dans les fin de test.

Lancer un seul test :
```bash
npm test supprimer-compte-utilisateur
```

### Syntaxe pour rédiger les tests 

Quand on code un test automatisé, il faut partir avec la structure suivante :

Etant donné ce contexte ...
Quand je  ...
Je m'attends à ... 

*Exemple :*
* *Etant donnée que j'ai un compte et que je suis sur la page principale du site*
* *Quand j'appuie sur le bouton "Sign In"*
* *Je m'attends à voir un formulaire avec le bouton "connecter"*

**Tous les tests sont dans un répertoire nommé "tests" et le fichier de test est nommé "NomFichier.test.js"**

* Se rendre sur une page 
```javascript
await page.goto('http://polr.campus-grenoble.fr');
```
* Attendre qu'un selecteur soit présent sur la page (conseiller pour éviter d'avoir une erreur dans l'action suivante) :
```javascript
await page.waitForSelector('nav[role="navigation"]');
```
* Cliquer sur un bouton 
```javascript
await page.click(".dropdown-toggle");
```
* Cliquer sur un bouton et ajouter un delai d'attente avant la prochaine action
```javascript
await page.click(".dropdown-toggle", {delay : 100});
```
* Renseigner un champ
```javascript
await page.type('input[name="username"]', 'admin');
```
* Renseigner un champ puis ajouter un delai d'attente avant la prochaine action 
```javascript
await page.type('input[name="username"]', 'admin', {delay : 100});
```
* Vérifier qu'une chaîne de caractère est présente dans une partie du DOM
```javascript
const htmlAdmin = await page.$eval('.login-name', e => e.innerHTML);
expect(htmlAdmin).toContain("admin");
```
* Faire un screenshot 
```javascript
await page.screenshot({path: './tests/img/acceder_stats_url/login_admin_stats_url.png'});
```
* Rechercher un élément par son texte dans une partie du DOM 
```javascript
await page.evaluate( () => {
    Array
    .from( document.querySelectorAll( '.dropdown-menu li a' ) )
    .filter( el => el.textContent === 'Dashboard' )[0].click();
});
```

#### Structure générale :

Structure générale :
* Une première variable "timeout" 

```javascript 
const timeout = 17000

// série de tests sur la page d'accueil
describe("Acceder aux stats des url avec un compte utilisateur", () => {
    let page

    //Créer un compte utilisateur
    test('Sign up', async () => {
        await page.goto('http://polr.campus-grenoble.fr')
        await page.waitForSelector('nav[role="navigation"]')
        // ...
       
    }, timeout)


    test('se deconnecter de marion1', async () => {
        await page.click('.login-name');
        await page.waitForSelector('.dropdown-menu');
        //...

    }, timeout)


    // cette fonction est lancée avant chaque test de cette
    // série de tests
    beforeAll(async () => {
        // ouvrir un onglet dans le navigateur
        page = await global.__BROWSER__.newPage()

        //Lorsqu'une boîte de dialogue s'ouvre, appuyer sur "ok" pour valider (très utile pour réussir à supprimer l'utilisateur)
        page.on('dialog', async dialog => {
            await dialog.accept();
        });

    }, timeout)

})
```



## Rédiger un ticket de bug




