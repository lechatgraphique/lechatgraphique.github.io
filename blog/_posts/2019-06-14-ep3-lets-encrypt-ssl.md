---
layout: post
title: "Étape 03 _ Sécuriser Nginx avec Let’s Encrypt (SSL) Ubuntu 18.04 LTS"
date: 2019-06-14 06:00:00 +0200
image : assets/images/blog/ssl.png
numberList: "06"
description: ""
---

Afin de sécuriser votre site avec un **Certificat SSL**, vous devez disposez d’un **nom de domaine** entièrement enregistré. J’utiliserai **example.com** tout au long de ce didacticiel.

Vous devez avoir les **deux enregistrements DNS** et configurés pour votre serveur. 

- Un **enregistrement A** avec **example.com** pointant sur l’adresse **IP publique** de votre serveur.
- Un **enregistrement A** avec **www.example.com** pointant sur l’adresse **IP publique** de votre serveur.

L'étape qui suis sera l'installation de **Let’s Encrypt** pour obtenir un **certificat SSL**. Dans notre cas nous utiliserons un logiciel **Certbot** sur votre serveur.

**Certbot** est en développement très actif. Les développeurs de **Certbot** conservent un référentiel de logiciels Ubuntu avec des versions à jour, nous allons donc utiliser ce référentiel.

Tout d’abord connectez-vous en **SSH** puis ajoutez le référentiel :

``` 
sudo add-apt-repository ppa:certbot/certbot
```

Vous devrez appuyer sur `ENTER` pour accepter.
Installez le paquet **Nginx** de **Certbot**.

```
sudo apt install python-certbot-nginx
```

**Certbot** est maintenant prêt à être utilisé, mais pour **configurer SSL** pour **Nginx**, nous devons vérifier une partie de la configuration de **Nginx**.

Certbot doit pouvoir trouver le **bloc serveur** correct dans votre **configuration Nginx** pour pouvoir **configurer automatiquement SSL**. Pour ce faire, il recherche une directive `server_name` correspondant au domaine pour lequel vous demandez un **certificat**.

Pour vérifier, ouvrez le fichier du **bloc serveur** de votre domaine.

```
sudo nano /etc/nginx/sites-available/example.com
```

Puis insérez le code ci-dessous : 

```
server {
        listen 80;
        root /var/www/html;
        index index.php index.html index.htm index.nginx-debian.html;
        server_name example.com;

        location / {
                try_files $uri $uri/ =404;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
        }
}
```

Recherchez la ligne existante `server_name`.
Mettez-le à jour pour qu’il corresponde à votre nom de domaine.

```
server_name example.com www.example.com;
```

Activez votre nouveau **bloc serveur** en créant un **lien symbolique** à partir du fichier de configuration de votre nouveau bloc serveur : 

```
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
```

Ensuite, dissociez le fichier de configuration par défaut du répertoire :

```
sudo unlink /etc/nginx/sites-enabled/default
```

**Enregistrez** le fichier et quittez votre éditeur. Vérifiez la syntaxe de vos modifications de configuration :

```
sudo nginx -t
```

Si vous obtenez une erreur, ouvrez de nouveau le fichier et recherchez les fautes de frappe ou les caractères manquants. Une fois que la syntaxe de votre fichier de configuration est correcte, **rechargez Nginx** pour charger la nouvelle configuration :

```
sudo systemctl reload nginx
```

**Certbot** peut maintenant trouver le bloc serveur correct et le mettre à jour.

**Certbot** fournit diverses méthodes pour obtenir des **certificats SSL** via des plugins. Le **plugin Nginx** se chargera de **reconfigurer Nginx** et de recharger la configuration chaque fois que nécessaire. Pour utiliser ce plugin, tapez ce qui suit :

```
sudo certbot --nginx -d example.com -d www.example.com
```

Ceci exécute **Certbot** avec le plugin —nginx, en utilisant -d pour spécifier les noms pour lesquels nous souhaitons que le certificat soit valide.

Si vous utilisez **Certbot** pour la première fois, vous serez invité à entrer une **adresse e-mail** et à accepter les conditions d’utilisation. Ensuite, **certbot** communiquera avec le **serveur Let’s Encrypt**, puis lancera un défi afin de vérifier que vous contrôlez le domaine pour lequel vous demandez un **certificat**.

Si cela réussit, **Certbot** vous demandera comment vous souhaitez configurer vos **paramètres HTTPS**.

```
Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
-------------------------------------------------------------------------------
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
-------------------------------------------------------------------------------
Select the appropriate number [1-2] then [enter] (press 'c' to cancel):
```

Sélectionnez votre choix puis appuyez sur `ENTRER`. La configuration sera mise à jour et **Nginx** se rechargera pour récupérer les nouveaux paramètres. **Certbot** se terminera par un message vous informant que le processus a abouti et où vos certificats sont stockés.

Les certificats de **Let’s Encrypt** ne sont valides que pendant **90 jours**. Cela encourage les utilisateurs à automatiser leur processus de renouvellement des certificats. Le paquet **Certbot** que nous avons installé s’occupe de cela en ajoutant un **scripT de renouvellement** à /etc/cron.d. Ce script s’exécute deux fois par jour et renouvellera automatiquement tout certificat dans les trente jours suivant l’expiration.

Pour tester le processus de renouvellement, vous pouvez effectuer un essai à blanc avec **Certbot** :

```
sudo certbot renew --dry-run
```

Si vous ne voyez aucune erreur, vous êtes prêt. Si nécessaire, **Certbot** renouvellera vos certificats et rechargera **Nginx** pour prendre en compte les modifications. En cas d’échec du processus de renouvellement automatique, **Let’s Encrypt** enverra un message au courrier électronique que vous avez spécifié pour vous avertir de l’expiration de votre certificat.
