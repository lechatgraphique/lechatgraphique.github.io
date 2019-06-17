---
layout: post
title: "Étape 05 _ Installer WordPress sur notre instance EC2"
date: 2019-06-15 06:00:00 +0200
image : assets/images/blog/wordpress.png
numberList: "08"
description: ""
---

Nous arrivons à la fin de ce didactitiel. 

**Récapitulation** des différentes tâches que nous avons effectuées.

- Création d'un compte **Amazon Web Services**
- Création d'une **base de données** avec **Amazon RDS**
- Création d'une **instance Amazon EC2**
- Configuration **SSL Nginx**

Maintenant nous allons **installer WordPress** sur notre **instance EC2**.

Connectez-vous à votre instance en **SSH** puis téléchargez **WordPress** :

```
cd /tmp
wget https://wordpress.org/latest.tar.gz
```

Une fois le téléchargement terminé, extrayez l’archive **WordPress** et déplacez les fichiers extraits dans le **répertoire racine** :


```
tar xf latest.tar.gz
sudo mv /tmp/wordpress/* /var/www/html
```

Enfin, nous devons définir les **autorisations appropriées** pour que le **serveur Web** puisse avoir un accès complet aux fichiers et **répertoires du site**.

Étant donné que **Nginx** et **PHP** s'exécutent en tant qu'utilisateur et groupe **www-data**, pour définir les **autorisations appropriées**, exécutez la commande **chown** suivante :

```
sudo chown -R www-data: /var/www/html
```

Nous devons également **autoriser MySQL** sur **l'instance EC2**. Connectez-vous à votre **espace AWS** et rendez-vous sur le **tableau de bord Amazon EC2**. Sélectionnez **« Groupes et sécurité »** à gauche de l’écran. Cliquer sur le **groupe RDS** et modifier **les entrées entrantes**. Dans le **champ source** veuillez renseigner **l'ID du groupe serveur EC2** puis **Enregistrer**.

![Amazon Web Service!](/assets/images/blog/blog-aws-rds-groups-mydsl.png)