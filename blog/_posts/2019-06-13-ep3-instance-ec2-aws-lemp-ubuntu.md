---
layout: post
title: "Étape 02 _ Créer une instance EC2 « LEMP » Ubuntu 18.04 LTS"
date: 2019-06-13 06:00:00 +0200
image : assets/images/blog/server.png
numberList: "04"
description: "Afin d’accéder aux différents services disponibles sur AWS, vous devez vous créer un compte. Je vous explique ci-dessous comment faire."
---
Aujourd'hui nous allons voir comment lancer et configurer notre instance **Amazon EC2** via la **Console AWS**. Une fois l’instance disponible nous lancerons le terminal afin de se **connecter en SSH** et d’installer la **Stack « LEMP »**.

Une fois connecté à votre espace **AWS Management Console** vous avez plusieurs options pour choisir un service. Soit par la recherche en tapant un **mot clé** où dans la liste des **Services AWS**. Nous allons rechercher le mot **EC2** et **cliquer dessus**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord.png)

Vous vous trouvez à présent sur le **Tableau de bord EC2**. Avant de lancer une instance nous allons créer deux choses indispensables : 

- Une paire de clés afin de vous connecter en `SSH`
- Un groupe de sécurité  pour les accès `SSH`, `HTTP`, `HTTPS`

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-ec2.png)

Commençons par la **paire de clés**. Dans le menu à gauche allez dans **Réseau et Sécurité** puis **Paire de clés**. 
Cliquez sur **Créer une paire de clés**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-paire-key.png)

Donnez lui un **nom** puis **créer** votre **paire de clés**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-paire-key-2.png)

Il vous demandera de **télécharger votre clé**.
**Enregistrer** à l’endroit que vous souhaitez. **Évité de la laisser dans votre dossier téléchargement**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-paire-key-3.png)

Nous allons passer à l’étape suivante. Création du **groupe de sécurité EC2**.
Rendez-vous dans le menu de gauche **Réseau et Sécurité** puis **Groupes de sécurité**. Comme pour la **paire de clés**, cliquez sur **Créer un groupe de sécurité**.

Renseignez le **nom du groupe** avec une **description**. Laissez le **VPS** par **défaut**.

Nous devons autoriser les entrées suivantes. `SSH`, `HTTP`, `HTTS`.  Une fois terminé cliquez sur **Créer**.

![Amazon Web Service!](/assets/images/blog/blog-aws-ec2-tableau-de-bord-group-security.png)

Nous avons terminé la configuration de notre **paire de clés** et notre **groupe de sécurité** ! 
Maintenant il est temps de lancer notre **instance EC2**.

Retournez sur le **Tableau de bord EC2**, puis cliquez sur **Lancer une instance**.

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

Cliquez sur **Vérifier et lancer**. Vous retrouvez un récapitulatif de toute la configuration de votre **Instance EC2**. Passez à l’étape **Suivante : Lancer**.

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

Nous en avons fini sur la configuration et le lancement de notre instance **Amazon EC2**. Dès à présent nous sommes près à configurer notre serveur web en SSH.