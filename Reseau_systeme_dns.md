# Réseau et Système


## DNS et Registrar

* **DNS : Domain Name System**
* Le DNS se charge de **convertir une adresse IP** (173.194.39.78) en un nom lisible : www.google.com 
* Les DNS se finissent pas un "." à la fin même si ce dernier n'apparaît pas sur le navigateur

Description : Les parties sont séparées par un point
* Extension : TLD (Top Level Domain) 
    * TLD nationaux (fr, it, de...)
    * TLD génériques (com, org, net...)
* Sous-domaine : google.fr est un sous-domaine de "fr."
* www : nom de la machine dans le domaine 

* **Registrar** : bureau d'enregistrement gérant la réservation des noms de domaine (ex : Gandi, OVH...)

## Configuration : pointer vers l'adresse IP du serveur 

* Enregistrement DNS : Ajouter
* Choisir "A" comme type d'enregistrement (A renvoie une adresse IPv4 pour un nom de host donné)
* Mettre un nom, par exemple : www (le site sera accessible depuis www.coffee-break.com) 
    * Mettre à jour le A avec un @ (@ = vide) pour le faire pointer sur notre serveur 
* Entrer l'adresse IP de notre serveur 

Types d'enregistrement : A, AAAA, Cname, MX, NS

## Créer des sous-domaines 

Sur le site Gandi, dans "Domaines/Enregistrement DNS", dans le fichier de zone, cliquer sur Editer et entrer :
* marion 1800 IN A 163.172.191.63 
    * le lien sera marion.coffee-break.pw
* enregistrer 

Sur le site Gandi, utiliser l'interface avec "ajouter"

## Créer un VirtualHost 

* Ouvrir un Bash
* Entrer dans le répertoire /etc/apache2/sites-available
* Copier le fichier "000-default.conf" en lui donnant le nom "marion.conf" : **cp 000-default.conf marion.conf**
* Entrer dans le fichier "marion.conf" et le mettre à jour :
    * ServerAdmin webmaster@localhost  (adresse pour envoyer les emails d'erreurs)
    * ServerName marion.coffee-break.pw    (lien du site)
    * DocumentRoot /var/www/html/marion/PHP_MachineCafe    (dossier où trouver le site sur le serveur)
    * DirectoryIndex machineCafe.php    (indiquer le fichier "index" à ouvrir)
* Activer le site : **a2ensite marion** 
* Relancer Apache : **systemctl reload apache2**

Visualisation du fichier marion.conf 
```
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        ServerName marion.coffee-break.pw
        DocumentRoot /var/www/html/marion/PHP_MachineCafe
                DirectoryIndex machineCafe.php

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```

[Ressource Site Debian Facile](https://debian-facile.org/doc:reseau:apache2:multisite)


# Mettre en ligne un projet Laravel

## Cloner le projet sur le serveur 

Une fois le projet cloné sur le serveur (git clone) :

Installer Composer dans le répertoire du projet :
```
apt-get update
apt-get install composer
```

Installer les dépendances nécessaires :
```
composer install
```
Copier le fichier ".env.example" et le renommer : 
```
cp .env.example .env
```
Générer la clé :
```
php artisan key:generate 
```
Mettre à jour le fichier .env :
```
nano .env
// mettre à jour les informations suivantes par exemple :
DB_DATABASE=nom BDD
DB_USERNAME=login
DB_PASSWORD=mdp
```


## Donner les droits à Apache 

Il faut donner les droits à Apache sur le dossier Storage du projet Laravel. Se rendre sur le **projet Laravel** puis : 
```
chown -R www-data:www-data storage/
```
Pour vérifier que l'utilisateur "www-data" (apache) posséde bien le dossier Storage :
```
ls -l storage/

// Il doit retourner par exemple 
drwxr-xr-x 3 www-data www-data 4096 Jan 30 09:25 app
drwxr-xr-x 2 www-data www-data 4096 Jan 30 09:25 debugbar
drwxr-xr-x 6 www-data www-data 4096 Jan 30 09:25 framework
drwxr-xr-x 2 www-data www-data 4096 Jan 30 11:17 logs
```
*-R permet d'appliquer la récursivité, c'est à dire, que tous les sous-dossiers de Storage auront la modification*

## Activer le "mod_rewrite"

Vérifier la présence du fichier "mod_rewrite.so", qui est normalement pré-installé avec Apache
```
ls -l /usr/lib/apache2/modules/
```
*Si on retrouve dans la liste le fichier c'est qu'il est bien pré-installé*

Créer un lien logique entre ce module et les fichiers de modules que comprend Apache
```
cd /etc/apache2/mods-available
sudo a2enmod rewrite
```
Ouvrir le fichier apache2.conf
```
sudo nano /etc/apache2/apache2.conf
```
Rajouter à la fin du fichier le code suivant pour s'assurer que le module sera bien actvité 
```
<ifModule mod_rewrite.c>
RewriteEngine On
</ifModule>
```
Redémarrer le serveur Apache 
```
systemctl reload apache2
```

## Paramètrer le VirtualHost 

Ajouter le code suivant pour que le fichier .htaccess (présent dans le projet Laravel) soit prioritaire par rapport aux configurations du VirtualHost. Permettant ainsi à Laravel d'activer les routes.

Ajouter à la fin du fichier marion-laravel.conf (/etc/apache2/sites-availables/) : 
```
<Directory /var/www/html/marion/Machine_Cafe>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
</Directory>
```

A noter, les configurations pour pointer vers la bonne page sont :
```
ServerName marion-laravel.coffee-break.pw
DocumentRoot /var/www/html/marion/machine_ilot_marion/public
    DirectoryIndex index.php
```

Relancer le serveur Apache 
```
systemctl reload apache2
```

## Supprimer la debugbar du site en ligne

Dans le fichier ".env" du projet, indiquer "false" : 
```
APP_DEBUG=false
```


# Chiffrer un site avec HTTPS 

**Avec Apache et Debian 9**

[Ressource](https://certbot.eff.org/#debianstretch-apache) 


Dans la racine du serveur (entrer "cd"), installer le package Certbot : **A réaliser uniquement la première fois**
```
sudo apt-get install python-certbot-apache -t stretch-backports
```

Lancer la commande : 
```
sudo certbot --authenticator webroot --installer apache
```
Puis ci-dessous les réponses à apporter aux différentes questions posées. A noter, l'ensemble des questions sont posées uniquement la première fois :
* Entrer un email 
```
Enter email address (used for urgent renewal and security notices) (Enter 'c' to
cancel): marion.chapuis@campus-numerique-in-the-alps.com
```
* Lecture des conditions : répondre "a"
```
Please read the Terms of Service at
https://letsencrypt.org/documents/LE-SA-v1.2-November-15-2017.pdf. You must
agree in order to register with the ACME server at
https://acme-v01.api.letsencrypt.org/directory
-------------------------------------------------------------------------------
(A)gree/(C)ancel: a
```
* Partager notre email avec des partenaires de Certbot : répondre "n"
```
Would you be willing to share your email address with the Electronic Frontier
Foundation, a founding partner of the Let's Encrypt project and the non-profit
organization that develops Certbot? We'd like to send you email about EFF and
our work to encrypt the web, protect its users and defend digital rights.
-------------------------------------------------------------------------------
(Y)es/(N)o: n
```
* Choisir le site concerné par son numéro : dans ce cas répondre "3"
```
Which names would you like to activate HTTPS for?
-------------------------------------------------------------------------------
1: ana.coffee-break.pw
2: marion.coffee-break.pw
3: marion-laravel.coffee-break.pw
4: seb.coffee-break.pw
5: sergio.coffee-break.pw
6: sergio-laravel.coffee-break.pw
-------------------------------------------------------------------------------
Select the appropriate numbers separated by commas and/or spaces, or leave input
blank to select all options shown (Enter 'c' to cancel): 3
```
* Confirmer le choix : répondre 1 
```
Select the webroot for marion-laravel.coffee-break.pw:
-------------------------------------------------------------------------------
1: Enter a new webroot
-------------------------------------------------------------------------------
Press 1 [enter] to confirm the selection (press 'c' to cancel): 1
```
* Entrer le chemin vers l'index de notre site : 
```
Input the webroot for marion-laravel.coffee-break.pw: (Enter 'c' to cancel): /var/www/html/marion/machine_ilot_marion/public/
```
* Choisir la redirection, c'est-à-dire que les visiteurs entrant "http" seront redirigés vers "https"
```
Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
-------------------------------------------------------------------------------
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
-------------------------------------------------------------------------------
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 2
```

Message de félicitations :-)

# Créer une clé SSH 

Sur la machine en local, générer la clé SSH, avec la commande dans un Bash :
```
ssh-keygen
```
Dans les questions : 
* Ne rien renseigner dans la question pour entrer une phrase (en effet, la clé SSH est là pour se connecter sans mot de passe)
* Entrer le mot de passe du serveur

Toujours sur la machine en local, copier la clé sur le serveur 
```
ssh-copy-id root@163..... // utilisateur@ip_serveur
```

Laisser un Bash avec le serveur ouvert (en cas de problème) et réouvrir un Bash pour tester la connexion en clé SSH

Les clés SSH sont disponibles dans le fichier :
```
.ssh/authorized_keys
```

**Lors du premier dépôt de clé SSH sur le serveur** :
Dans le fichier "sshd_config" disponible dans le dossier /etc/ssh/, décomenter la ligne : 
```
PubkeyAuthentication // supprimer le # pour décommenter
```


