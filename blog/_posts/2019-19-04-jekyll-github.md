---
layout: post
title: "Jekyll et Github"
date: 2019-04-19 12:00:00 +0200
image : assets/images/blog/jekyll.png
numberList: "02"
description: "Jekyll est un outil développé en Ruby qui permet de générer des pages statiques à partir de plusieurs fichiers
Le principal intérêt du système est qu’il permet de publier simplement un site car il génère des fichiers HTML."
---

Tout d’abord il existe un tas d’outils pour créer des blogs.  Le plus répandu étant **WordPress**. **WP** embarque beaucoup de fonctionnalités de base et peu être personnalisable dans touts les sens **(plugins, thèmes etc.)**. Le problème c’est loin d’être idéal à maintenir, à faire évoluer ou à exploiter au quotidien.

Dans mon cas d'utilisation, j’ai donc décidé de tout mettre en commun avec une seule technologie qui correspondait à mes besoins et mes envies, c’est ainsi que je me suis tourné vers  [Jekyll](https://jekyllrb.com/). 

## Qu'est-ce que Jekyll ?
**Jekyll** est un outil développé en Ruby qui permet de générer des pages statiques à partir de plusieurs fichiers [Markdown](https://daringfireball.net/projects/markdown/)  ou  [Liquid](https://github.com/Shopify/liquid/wiki) . 
Le principal intérêt du système est qu’il permet de publier simplement un site car **il génère des fichiers HTML**. On comprend alors vite pourquoi cette technologie est très intéressante à l’usage.

## Performances  
**Jekyll** compile notre site. On obtient donc un ensemble de **pages HTML statiques**. Contrairement à un CMS comme **WordPress**, les pages n’ont pas besoin d’être générées à chaque visite. Il n’y a pas de connexion à une base de données qui prend une éternité pour faire toujours les mêmes requêtes etc. Ainsi, nous nous retrouvons avec une fluidité vraiment agréable et l’expérience n’en est que meilleur pour l’utilisateur. 

## Sécurité
Comme je le disais plus haut, **Jekyll compile des pages HTML**. Il coule sous le sens qu’il y aura **aucun souci de sécurité direct**. Il n’y a pas de mise à jour à faire pour combler des **failles de sécurité**. Il n’y a pas de code à maintenir et pas de **mise à jour PHP où MySQL**. De plus avec **Jekyll**, un seul dossier très léger peut être **sauvegardé** et **transféré** sur le *cloud* ou *Github*.

## Déploiement 
Une fois l’ensemble compilé, **vos pages** et **vos assets** se retrouvent dans un seul et même dossier nommé `_site`. Bien entendu, vous pouvez compiler l’ensemble autant de fois que vous le souhaitez, il suffira alors de prendre ce dossier et de le mettre sur votre **FTP** pour que tout fonctionne. C’est la seule chose à faire et c’est parfaitement **transparent pour les utilisateurs**.

Si vous utilisez un système de **gestion de version** comme **Git**, sachez que beaucoup de services s’occupent de l’hébergement pour vous, il suffira de `push` votre code sur le repository distant et le site sera compilé pour vous. 

* Le plus connu étant  [Github Pages](https://pages.github.com/).

Pour ma part j’héberge le blog avec mon **dépôt Git Hub**. Cela permet **de versionner facilement** et d’avoir un **hébergement gratuit** :).

## Création des articles
**Jekyll** est pensé pour utiliser le **Markdown** lors de l’écriture d’un article ou d’une page. Il **convertit nativement** vos fichiers **markdown** en **page HTML**. C’est super pratique, car il n’y a plus besoin de se connecter à une interface. Il suffit d’ouvrir un fichier texte et vous êtes prêt à écrire. Mais aussi plus besoin de connexion internet ou d’un ordinateur. Désormais, je commence souvent mes articles sur **mon iPhone** avec l’application [Bear](https://bear.app/), car la **syntaxe markdown** évite d’avoir une interface complexe pour faire de la mise en forme.

## Design CSS
Un point vraiment très intéressant c’est que **Jekyll**  [intègre nativement](https://jekyllrb.com/docs/assets/) un support pour [Sass](https://sass-lang.com/guide) et de  [CoffeeScript](https://coffeescript.org/)  (avec une gem). L’utilisation de **SASS** ce fait très facilement. 

Je peux que vous recommander là [documentation Jekyll](https://jekyllrb.com/docs/) si vous souhaitez plus d’informations. 

Si j’ai le temps je ferais un article sur l’installation et le déploiement d’un site avec Jekyll :).

J’espère avoir été clair sur les raisons qui m’ont poussé à effectuer ce choix, si vous avez des questions n’hésitez pas à les poser à l’adresse : **infos@lechatgraphique.fr**

Merci et à bientôt :).