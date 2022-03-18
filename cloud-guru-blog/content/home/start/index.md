---
image: the-adventure-begins.jpg
title: Démarrez ici !
date: '2022-03-07'
lastmod: '2022-03-18'
aliases:
  - start
  - starthere
menu:
    main: 
        weight: -85
        params:
            icon: flag
showLeftSidebar: true
comments: false
---

Bienvenue sur **Cloud-Guru, le Blog** !

## Présentation (très) générale

Cela fait bien longtemps que j'aurais du démarrer ce blog; bien longtemps... Mais ne dit-on pas : ***Il n'est jamais trop tard pour commencer*** ? Alors, voilà, je m'y mets et j'espère le faire avec sérieux (je parle ici de régularité), mais surtout avec enthousiasme. Sérieusement, oui, mais sans se prendre au sérieux, justement 😛. Cela est et devra rester un plaisir.

L'objectif de **Cloud-Guru, le Blog** est de partager mes connaissances dans le domaine du ***Cloud***, mais aussi sur de nombreux autres domaines parmi ceux listés ci-dessous :

- *Architectures*, *Infrastructures* et *Urbanismes*
- *Azure*, *GCP* et d'autres *Cloud Public*
- *Méthodes Agiles*, *approches DevSecOps* et *SRE* et bien d'autres concepts du même ordre
- *Git*, *pipelines*, *CICD* et de nombreux sujets qui s'y rapportent.
- *Azure DevOps Wiki*, *Board*, *Repos*, *Pipelines* et plus si affinités.
- *IaC* (**I**nfrastructure **a**s **C**ode), *Terraform*, *Azure Bicep* et de nombreux outils de tests, de qualité de code ou autres joyeusetés.
- *Templating Handlebars* et son utilisation dans le monde de l'**IaC**, des systèmes et de l'IT au sens large.
- La sécurité. Elle est nécessaire partout. **By design** comme disent nos amis outre-atlantique où outre-manche.
- Et bien d'autres, à venir, je pense. 😛

## Créer un démonstrateur comme fil conducteur

L'idée, qui me motive sur la publicaton régulière d'articles sur ce blog, est de présenter des exemples réalistes correspondants à l'implémentation d'un ***démonstrateur*** dans les clouds ***Azure*** et ***GCP*** (que je connais bien), mais aussi sur le cloud ***AWS*** (que je n'ai jamais implémenté en production).

**Voici ci-dessous un schéma très simple représentatif de ce démonstrateur:**

![Démonstrateur](img/demonstrator.jpg)

**Description fonctionnelle de ce démonstrateur:**

| # |Item|Description|
|:-:|----|-----------|
|1|Simple Application| La finalité de ce démonstrateur est bien sur de partager quelques éléments techniques et les bonnes pratiques pour les mettre en oeuvre dans le Cloud (mais aussi ailleurs). Toutefois le besoin premier est de répondre à une attente métier qui se présente dans la grande majorité des cas sous la forme d'une application. 🤗|
|2|Landing Zone|L'application en question est posée sur ce que l'on appelle communément une **Landing Zone**. Un article dédié détaillera ce sujet. En attendant, notre ami [Google](https://www.google.com/search?q=landing+zone) devrait pouvoir vous aider à répondre à vos intérogations.|
|3|Datacenter|Le datacenter, modélisé ici par un simple rectangle, représente la catégorie ***Non Cloud*** d'une partie de l'**Infrastructure** du SI d'Entreprise. Souvent appelé "On Premise" ou "Legacy" dans notre jargon informatique, ce dernier n'est en rien synonyme d'**obsolète*. En tout cas, par systématiquement.|
|4,5,6|WAN, Internet et DL|Ces trois éléments représentent le réseau WAN du SI d'Entreprise (géré le plus souvent par un opérateur comme par exemple [Equinix](https://www.equinix.fr), [Colt](https://www.colt.net) ou [Orange](https://www.orange-business.com/fr)), Internet (que l'on ne présente plus) et un liaison privée (**P**rivate **L**ink) entre le datacenter ***Non Cloud*** et la **Landing Zone**.|
|A,B,C|Cloud Providers Azure, GCP et AWS|Ce démonstrateur devra pouvoir s'implémenter chez les trois principaux **Cloud Providers** que sont **Azure**, **GCP** et **AWS**.|

## Mon environnement de travail

### Schéma représentatif

![Environnement de Dev](img/dev-environment.jpg)

### Description des composants

| # |Item|Description|
|:-:|----|-----------|
|1,A|gandi.net|L'ensemble des noms de domaines que je détiens sont gérés par **gandi.net**. Cette société française propose aussi l'hebergement de sites Internet, la production de certificats SSL, l'hébergement de boites mails (liés aux noms de domaines) et une offre Cloud basée sur de l'OpenStack.|
|2,B,C|Github|Mes diffétents **repositories** [**B**] privés et publics sont hébergés chez **Github**. Ce blog y est d'ailleurs hébergé par l'intermédiaire des ***GitHub Pages*** [**C**]. GitHub propose de nombreux autres composants DevOps comme les ***issues*** (utilisé via la ***GitHub apps*** [utterances](https://github.com/apps/utterances) pour laisser un commentaire sur ce Blog), les ***wiki***, ou les ***actions***.|
|3,D,E,F,G,H|Azure DevOps|J'utilise **Azure DevOps** comme plateforme de CICD. De nombreux éléments peuvent être construit ***As Code*** avec l'outil désormais bien connu ***Terraform*** de ***Hashicorp***. Pour le moment j'utilise essentiellement les composants ***Repos*** [**E**] et ***Pipelines*** [**F**] au sein d'un ***Project Azure DevOps***. ***Boards*** [**D**] est un très bon outil de développement Agile sur lequel je reviendrai surement. ***Artifacts*** [**H**] est un gestionnaire de packages. ***Test Plans*** [**G**] est un outil de gestion de tests permettant de s'assurer qu'une noubelle fonctionnalité réponds au besoin sans provoquer de regressions sur les autres fonctionnalités d'un produit. Il permet notamment d'automatiser les tests manuels.|
|4,5,6|Cloud Providers Azure, GCP et AWS|J'ai souscrit un abonnement sur ces trois **Cloud Providers**. L'abonnement est lié à un moyen de paiement, mais comme le modèle de facturation du Cloud est le **P**ay **A**s **Y**ou **G**o (paiement à l'usage), il est tout à fait possible de tester et de de construire de nombreuses choses sans que cela ne revienne cher (<<50€ par mois). Attention toutefois, il faut rester prudent car la facture peut rapidement devenir importante selon les composants utilisés. ***Microsoft***, ***Google*** et ***Amazon*** ont mis en place des versions de leurs composants dédiés au développement qui sont en général peu coûteux.|
|7,I,J|Synology DSM|J'ai un **DSM** à la maison. Il me permet notamment d'héberger des ***containers*** [**J**] et faire tourner quelques VM sur ***Virtual Machine Manager*** [**I**]. C'est un produit très intéressant pour tester tout un tas de choses facilement et simuler un datacenter ***Non Cloud***.|
|8,K,L,M|Laptop|Enfin, je possède un **Macbook Pro** qui me sert pour la bureautique et comme poste de développement. Mes principaux outils sont ***VSCode*** [**K**] et ***Desktop Docker Engine*** [**L**] pour tester mes containers en local. Ensuite, j'installe l'ensemble des outils de développment [**M**] nécessaires pour mes **P**roof **O**f **C**oncepts.|

### Environnement de DEV standard

> Si l'on souhaite définir, un environnement de DEV standard, une très bonne solution est de le faire depuis un container comportant l'ensemble des outils nécessaires et suffisants. Avec une image, il est ainsi très facile de faire en sorte qu'une équipe de DEV travaille avec le même environnement correspondant à celui de production.

## Et ensuite ?

Et, bien, il ne me reste plus qu'a me mettre au travail. Rendez-vous sur des prochains articles à suivre...

![Hop, au boulot !](img/lets-get-started.jpg)

