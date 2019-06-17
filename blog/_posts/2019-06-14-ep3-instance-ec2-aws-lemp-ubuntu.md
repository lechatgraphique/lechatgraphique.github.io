---
layout: post
title: "Étape 03 _ Créer une instance EC2 « LEMP » Ubuntu 18.04 LTS"
date: 2019-06-14 06:00:00 +0200
image : assets/images/blog/server.png
numberList: "06"
description: "Comment créer et configurer une instance Amazon EC2 avec Nginx"
---
Aujourd’hui nous allons voir comment lancer et configurer notre **instance Amazon EC2**. Une fois l’instance disponible nous lancerons le **terminal** afin de se connecter en **SSH** et installer la **Stack « LEMP »**.

Une fois connecté à votre espace **AWS Management Console** vous avez plusieurs options pour sélectionner un service. Soit par la recherche en tapant un **mot-clé** ou dans la liste des **Services AWS**. Rechercher le mot **EC2** et cliquer dessus.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord.png)

Vous êtes dès à présent sur le **tableau de bord Amazon EC2**. Sélectionnez **« Instances »** dans le coin gauche de l’écran.

Nous allons ensuite créer une **nouvelle instance EC2**. Cliquez sur le bouton **Lancer une instance**. 

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ec2-instance.png)

On vous propose de choisir une image (AMI). Pour notre installation, nous allons choisir **Ubuntu Server 18.04 LTS (HVM), SSD Volume Type** en **64bits (x86)**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami.png)

Choisissez le type éligible à **l’offre gratuite** puis cliquez sur le bouton **Suivant : Configurer les détails de l’instance**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami-2.png)

Vous n’avez rien de particulier à faire sur cette page de configurations. Passez à l’étape **Suivante : Ajouter du stockage**.

Avec **l’offre gratuite** vous avez au **maximum 30 Go d’offert**. Passez à l’étape **Suivante : Ajouter des balises**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami-3.png)

Je passe volontairement l’étape des **balises**. Si vous souhaitez **plus d'informations** dessus : [Balises des ressources Amazon EC2](https://aws.amazon.com/fr/premiumsupport/knowledge-center/ec2-resource-tags/).

Passez à l’étape **Suivante : Configurer le groupe de sécurité**. 

Afin de donner les accès `SSH`, `HTTP`, `HTTS` nous devons établir quelques **règles de connexions**. Créez un nouveau **groupe de sécurité** et **renommez-le**. Autorisez les entrées suivantes. `SSH`, `HTTP`, `HTTS`.  Une fois terminé, cliquez sur **Vérifier et lancer**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami-4-groups.png)

Vous retrouvez un **récapitulatif**  de toute la configuration de votre **instance EC2**. Passez à l’étape **Suivante : Lancer**.

On vous demande de sélectionner une **paire de clés**. Créez une nouvelle **paire de clés**, **nommez-la** et **téléchargez-la**. Enregistrez votre **paire de clés** à un endroit tel que votre dossier `/.ssh` par exemple.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami-5-key.png)

Pour suivre **l’état de votre instance** rendez-vous sur le **tableau de bord Amazon EC2** puis sélectionnez vos **instances**.

Vous pouvez voir que l’instance est en **État : Running**. Cela veut dire que tout fonctionne bien.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami-6.png)

Un point **très important**. **AWS** vous attribue un **IPv4** pour avoir accès à votre site. Cependant cette IP changera à chaque **redémarrage** du serveur. Vous pouvez pallier ce problème en attribuant une **IP Elastic** à votre instance.

Allez sur votre **tableau de bord Amazon EC2**. Sélectionnez « **IP Elastic** » à gauche de l’écran. Une fois sur la page cliquez sur le bouton **Allouer une nouvelle adresse**.

Laissez le **Pool Amazon** par **défaut** et faites **Allouer**.


Vous avez créer votre **IP Elastic**. Il ne vous reste plus qu'à associer votre **IP à votre Instance EC2**. Clique droit sur votre **IP Elastic** puis **Associer l’adresse**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ip-elastic.png)

Dans le menu déroulant choisissez votre **ID d’instance**, puis **Associer**. 

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ip-elastic-1.png)

Retournez dans vos **instances**. Vous remarquerez que votre ancienne **IPv4** a changé. Elle à été remplacée par votre **IP Elastic**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ip-elastic-2.png)

Dès à présent nous sommes prêt à configurer notre **serveur web** en **SSH**.

Pour trouver vos identifiants de **connexion SSH** vous devez être sur votre **liste d’instances** et sélectionner votre **instance**. En haut cliquez sur le bouton **Connexion**.

Une fenêtre s’ouvre en vous indiquant tout ce dont vous avez besoin pour vous **connecter en SSH**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-indentifiant-ssh.png)

Ouvrez votre **terminal**. 

Votre clé ne doit pas être visible publiquement pour que SSH fonctionne. 

Utilisez cette commande :

```
chmod 400 votre_paire_de_clés.pem
```

Puis connectez-vous en **SSH** :

```
ssh -i "votre_paire_de_clés.pem" ubuntu@ec2-34-254-124-182.eu-west-1.compute.amazonaws.com
```

Si votre **paire de clés** est dans un dossier spécifique, indiquez le **PATH** complet. Par exemple :

```
ssh -i "/Users/bastienclement/Documents/votre_paire_de_clés.pem" ubuntu@ec2-34-254-124-182.eu-west-1.compute.amazonaws.com
```
 
Vous devez vous retrouver comme ci-dessous :

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-terminal.png)

Commencez à mettre à jour **l’index des paquets** de votre serveur.

``` 
sudo apt update
```

Ensuite, installez le **serveur Nginx**.

``` 
$ sudo apt install nginx
```

Une fois **Nginx** installé, tapez **l’adresse de votre site** ou **IP Elastic** dans votre navigateur. 

La page de destination par défaut de Nginx apparaît :

``` 
http://serveur_domaine_ou_ip.com
```
![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-page-nginx.png)

Si vous voyez la page ci-dessus, vous avez correctement installé **Nginx**.

Étant donné que **Nginx** ne contient pas de traitement **PHP natif**, contrairement à certains autres serveurs Web, vous devrez installer `php-fpm`, qui signifie « fastCGI process manager ». Nous dirons à Nginx de transmettre les **requêtes PHP** à ce logiciel pour le traitement.

Installez les modules `php-fpm`, `php-mysql`, qui permettront à **PHP de communiquer avec votre base de données**. L’installation utilisera les fichiers de base de PHP nécessaires :

```
$ sudo apt install php-fpm php-mysql
```

Dans la prochaine étape nous allons **Sécuriser Nginx avec Let’s Encrypt (SSL)**. **Cette étape n’étant pas obligatoire** vous pouvez directement passer à l’étape suivante **« Installer WordPress sur notre instance EC2 »**. Cependant si vous souhaitez suivre la **sécurisation Nginx** vous devez disposer d’un **nom de domaine**.
