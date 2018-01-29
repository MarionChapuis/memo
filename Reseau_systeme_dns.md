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







