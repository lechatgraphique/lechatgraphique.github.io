---
layout: post
title: "Étape 02 _ Créer une instance EC2 « LEMP » Ubuntu 18.04 LTS"
date: 2019-06-13 06:00:00 +0200
image : assets/images/blog/server.png
numberList: "05"
description: ""
---
Aujourd'hui nous allons voir comment lancer et configurer notre instance **Amazon EC2** via la **console AWS**. Une fois l’instance disponible nous lancerons le terminal afin de se **connecter en SSH** et installer la **Stack « LEMP »**.

Une fois connecté à votre espace **AWS Management Console** vous avez plusieurs options pour sélectionner un service. Soit par la recherche en tapant un **mot-clé** ou dans la liste des **Services AWS**. Rechercher le mot **EC2** et **cliquer dessus**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord.png)

Vous vous trouvez à présent sur le **tableau de bord EC2**. Avant de lancer une instance nous allons créer deux choses indispensables : 

- Une paire de clés afin de vous connecter en `SSH`
- Un groupe de sécurité  pour les accès `SSH`, `HTTP`, `HTTPS`

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ec2.png)

Commençons par la **paire de clés**. Dans le menu à gauche allez dans **Réseau et Sécurité** puis **Paire de clés**. 
Cliquez sur **Créer une paire de clés**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-paire-key.png)

Donnez-lui un **nom** puis **créer** votre **pair de clés**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-paire-key-2.png)

Il vous demandera de **télécharger un fichier en .pem**.
**Enregistrer** à l’endroit que vous souhaitez. **Évité de la laisser dans votre dossier téléchargement**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-paire-key-3.png)

Nous allons passer à l’étape suivantes. **Groupe de sécurité EC2**.
Rendez-vous dans le menu de gauche **Réseau et Sécurité** puis **Groupes de sécurité**. Comme pour la **paire de clés**, cliquez sur **Créer un groupe de sécurité**.

Renseignez le **nom du groupe** avec une **description** puis laissez le **VPS** par **défaut**.

Nous devons autoriser les entrées suivantes. `SSH`, `HTTP`, `HTTS`.  Une fois terminé cliquez sur **Créer**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-group-security.png)

Nous avons terminé la configuration de notre **paire de clés** et notre **groupe de sécurité** ! 
Maintenant il est temps de lancer notre **instance EC2**.

Retournez sur le **tableau de bord EC2**, puis cliquez sur **lancer une instance**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ec2.png)

On vous proposent de choisir une **image (AMI)**. Nous allons choisir **Ubuntu Server 18.04 LTS (HVM), SSD Volume Type** en **64bits (x86)**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami.png)

Choisissez le type éligible à **l’offre gratuite** puis faite **Suivant : Configurer les détails de l’instance**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami-2.png)

Vous n’avez rien de particulier à faire sur cette configuration. Passez à l’étape **Suivante : Ajouter du stockage**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami-3.png)

Je passe volontairement l’étape des **balises**. Si vous souhaitez plus d'information dessus : [Balises des ressources Amazon EC2](https://aws.amazon.com/fr/premiumsupport/knowledge-center/ec2-resource-tags/).

Passez à l’étape **Suivante : Configurer le groupe de sécurité**. Comme nous avons déjà crée notre **groupe de sécurité**, nous avons juste à sélectionner un **groupe de sécurité existant** et cocher notre **ID de groupe de sécurité**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami-4.png)

Cliquez sur **Vérifier et lancer**. Vous y retrovuerez un récapitulatif de toute la configuration de votre **Instance EC2**. Passez à l’étape **Suivante : Lancer**.

On vous demande de sélectionner une **paire de clés**. Comme nous l’avons fait au préalable, choisissez votre **clés** et **Lancer votre instance**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami-5.png)

Voila votre instance est en cours de lancement. Allez sur **Afficher les instance**. 

Vous pouvez voir que l’instance est en **État : Running**. Cela veut dire que tout fonctionne bien.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ami-6.png)

Un point très **important**. **AWS** vous attribue un **IPv4** pour avoir accès à votre site. Cependant cette IP changera à chaque redémarrage du serveur. Vous pouvez pallier à ce problème en attribuant une **IP Elastic** à votre instance ce qui aura pour effet d’avoir une **IP Fixe**. 

Allez dans le menu de gauche dans **Réseau et sécurité** puis **Adresse IP Elastic**. **Allouer une nouvelle adresse**. 

Laissez le **Pool Amazon** par **défaut** et faite **Allouer**.

Vous avez crée votre **IP Fixe**. Il vous reste plus qu'à **associer votre IP** à votre **Instance EC2**. **Clique droit** sur votre **IP Elastic** puis **Associer l’adresse**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ip-elastic.png)

Dans le menu déroulant choisissez votre **ID d’instance**, puis **Associer**. 

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ip-elastic-1.png)

Retournez dans vos instances. Vous remarquerez que votre ancienne **IPv4** a changé et devenue bleu. Elle à été remplacé par votre **IP Elastic**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ip-elastic-2.png)

Nous en avons fini sur la configuration et le lancement de notre instance **Amazon EC2**. Dès à présent nous sommes près à configurer notre **serveur web** en **SSH**.

Pour trouver vos identifiants de connexion **SSH** vous devez sélectionner votre instance. En haut de votre navigateur cliquer sur le bouton connexion.
Une fenêtre s’ouvre en vous indiquant tout ce que vous avez besoin pour vous connectez en **SSH**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-indentifiant-ssh.png)

Ouvrez votre **terminal**. Votre clé ne doit pas être visible publiquement pour que SSH fonctionne. Utilisez cette commande :

```
chmod 400 votre_paire_de_clés.pem
```

 Puis connectez-vous en **SSH** :

```
ssh -i "votre_paire_de_clés.pem" ubuntu@ec2-34-254-124-182.eu-west-1.compute.amazonaws.com
```

Si votre paire de clés est dans un dossier spécifique, indiquez le **PATH** complet. Par exemple :

```
ssh -i "/Users/bastienclement/Documents/votre_paire_de_clés.pem" ubuntu@ec2-34-254-124-182.eu-west-1.compute.amazonaws.com
```
 
Vous devez vous retrouvez comme ci-dessous :

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-terminal.png)

Commencez à mettre à jour **l’index des paquets** de votre serveur.

``` 
sudo apt update
```

Ensuite, **installez** le serveur Nginx.

``` 
sudo apt install nginx
```

Une fois **Nginx** installer, tapez **l’adresse de votre site** ou **IP Elastic** dans votre navigateur. La page de destination par défaut de Nginx apparaît :

``` 
http://serveur_domaine_ou_ip.com
```
![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-page-nginx.png)

Si vous voyez la page ci-dessus, vous avez correctement installé Nginx.

Maintenant que vous avez votre serveur Web, vous devez installer **MySQL**. Dans notre cas nous installons juste les dépendances afin de connecter plus tard notre base de données **Amazon RDS.**

Installez **MySQL Server** : 

```
sudo apt install mysql-server
```

Vous n’avez rien d’autre à faire pour **MySQL**.

Étant donnée que **Nginx** ne contient pas de **traitement PHP** natif, contrairement à certains autres **serveurs Web**, vous devrez installer `php-fpm`, qui signifie **« fastCGI process manager »**. Nous dirons à Nginx de transmettre les requêtes PHP à ce logiciel pour le traitement.

Installez le module `php-fpm`, `php-mysql`, qui permettra à PHP de communiquer avec votre base de données. L’installation utilisera les fichiers de base de PHP nécessaires :

```
sudo apt install php-fpm php-mysql
```

Dans la prochaine étape nous allons **Sécuriser Nginx avec Let’s Encrypt (SSL)**. **Cette étape n'étant pas obligatoire** vous pouvez directement passer à l'étape **« Créer une base de données MySQL avec RDS »**. Cepandant si vous souhaitez suivre la **sécurisation Nginx** vous devez disposez d'un **nom de domaine**. 
