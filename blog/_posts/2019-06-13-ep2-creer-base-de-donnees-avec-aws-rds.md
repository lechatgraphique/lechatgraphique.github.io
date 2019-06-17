---
layout: post
title: "Étape 02 _ Créer une base de données MySQL avec RDS"
date: 2019-06-13 06:00:00 +0200
image : assets/images/blog/mysql.png
numberList: "05"
description: "Apprenez à mettre en place une base de données externe avec Amazon RDS"
---

Dans cette **deuxième étape** nous allons préparer notre **base de données WordPress**. 

Nous allons avoir **deux instances distinctes** :

- Une **instance RDS** Avec **MySQL** afin d'héberger nos données **WordPress**
- Une **instance EC2** avec notre **serveur web Nginx** ainsi que les fichiers sources **WordPress**

Connectez-vous à **compte AWS** et via la **console** rechercher le **service RDS**.

![Amazon Web Service!](/assets/images/blog/blog-aws-rds-search-rds.png)

Vous êtes des à présent sur le **tableau de bord Amazon RDS**. Sélectionnez **« Bases de données »** dans le coin gauche de l’écran.

Nous allons ensuite créer une **nouvelle instance MySQL**. Cliquez sur le bouton **Créer une base de données**. 

![Amazon Web Service!](/assets/images/blog/blog-aws-rds-tableau-de-bord-rds.png)

Assurez-vous de sélectionner **MySQL** et de cocher la case **« N’activer que les options éligibles pour le niveau d’offre gratuite RDS »** puis passez à l'étape **suivante**.

![Amazon Web Service!](/assets/images/blog/blog-aws-rds-select-mysql.png)
![Amazon Web Service!](/assets/images/blog/blog-aws-rds-select-mysql-opt.png)

Vous vous trouvez dans la page des **spécification de détails de base de données**.

En ce qui concerne les **spécifications de l’instance** vous pouvez laissez les options par **défaut**. Nous allons nous intéressez aux **paramètres**. Renseignezles différents champs demander puis faites **suivant**.

![Amazon Web Service!](/assets/images/blog/blog-aws-rds-params.png)

Dans les options **réseau et sécurité** laisser tout par **défaut**.

![Amazon Web Service!](/assets/images/blog/blog-aws-rds-reseau-securite.png)

Dans les options de **base de données**, nous allons créer le **schéma** pour notre futur **WordPress**. Indiquez un **nom de base de données** puis laissez les autres options par **défaut**.

![Amazon Web Service!](/assets/images/blog/blog-aws-rds-name-db.png)

Le reste des options tels que **chiffrement**, **sauvegarde**, **supervision** etc. Laissez tout par **défaut** puis cliquer sur le bouton **Créer une base de données**.

Votre instance est en **cours de création**, cela prend quelques minutes avant que soit complètement **opérationnel**.

![Amazon Web Service!](/assets/images/blog/blog-aws-rds-create.png)

Pour suivre **l’état de votre instance** rendez vous sur le **tableau de bord Amazon RDS** puis sélectionnez vos **base de données**.

![Amazon Web Service!](/assets/images/blog/blog-aws-rds-tableau-de-bord-rds-run.png)

Nous reviendrons plus tard dessus après la création de notre **instance Amazon EC2**. Gardez bien vos **identifiants**, nous en aurons besoin pour établir la connexion avec notre serveur WordPress.