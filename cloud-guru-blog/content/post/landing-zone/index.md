---
image: landing-zone-title.jpg
title: "Landing Zone"
date: 2022-03-26
# lastmod: 2022-03-26
categories:
  - cloud
  - archi
# hidden: true
# draft: true
---

## Avant-propos

Mes premiers pas, comme architecte technique dans le Cloud, datent de 2014 lorsque que Microsoft a renommé sa ***Windows Azure Platform*** en ***Microsoft Azure***. Microsoft a proposé, cette même année, son nouveau modèle de déploiement ***ARM*** en remplacement de que l'on appelle depuis le modèle ***Classic***. Ce dernier devrait disparaître en 2023.

L'***Infrastructure as Code*** en était vraiment à ses débuts et la maturité d'Azure n'était pas ce qu'elle est aujourd'hui. Je travaillais alors avec un de mes collègues développeur systèmes et à chaque nouvelle évolution d'ARM, nous devions adapter nos templates ARM et nos scripts powershell pour maintenir les quelques infrastructures applicatives installées sur Azure.

Quelques années plus tard, en 2017, dans le cadre d'une mission longue chez un ***géant de la grande distribution***, j'ai commencé à travailler sur la définition d'un ***socle Cloud*** permettant d'accueillir plusieurs centaines de leurs applications dans le cadre d'un grand programme de transformation digitale de l'Entreprise.

À ce moment là, il n'existait encore aucune ***bonnes pratiques***, ni ***principes fondateurs*** pour définir un SI d'Entreprise dans le Cloud Azure et clairement, la plateforme de Microsoft n'était pas encore prête pour répondre pleinement à ce type de besoin. Nous avons donc du nous adapter et proposer un modèle permettant d'accueillir plusieurs équipes différentes sur un même espace Cloud partagé en respectant un fort cloisonnement technique et des règles de sécurité définies par le RSSI responsable du domaine ***Cloud***.

En juillet 2017, après de nombreux échanges avec la ***CAT Team de Microsoft***, nous avons réussi à définir un modèle et un prototype qui a permis de montrer sa robustesse en portant quelques applications pilotes et la plateforme de CICD de l'Entreprise. Un premier document Microsoft [Azure Virtual Datacenter](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/resources/vdc) est sorti en novembre de cette même année. Les fondations et les bonnes pratiques pour définir un Cloud d'Entreprise s'étoffaient. Nous avions le sentiment d'avoir participé, à notre échelle, à celles-ci. 🤗

En 2018, nous avons mis en place l'instance de production qui héberge notamment leur site de ***e-commerce*** encore aujourd'hui. Si notre ***socle Cloud*** était robuste, son code **terraform** était difficile à faire évoluer. Toutefois, les principes étaient bons et nous avons pu les reproduire chez Google en 2019 pour héberger leur ***Data lake***. Nous avons amélioré notre qualité de code terraform (en nous appuyant sur du templating [Handlebars](https://handlebarsjs.com)) garantissant cette fois une maintenabilité optimale.

Aujourd'hui, les ***Cloud Providers*** proposent leur définition de ces fondations et de ces bonnes pratiques. Souvent appelées Landing Zone ou Cloud Foundation.

Cet article en présente les grands principes et les éléments clefs.



## Définition générique d'une Landing Zone

Nous pouvons définir une Landing Zone (ou Cloud Fondations), comme la prise en compte dans le Cloud, des principes fondateurs proposés dans le schéma ci-dessous et précisés dans les chapitres suivants. Cette définition n'est pas normalisée (au sens ISO du terme). Celle-ci n'est donc pas unique. Il faut éventuellement l'adapter à son propre besoin. Elle a l'ambition toutefois de définir une base de réflexion et d'amélioration.

### Schéma

![Landing Zone](landing-zone.jpg)

### Explications générales

La définition d'une ***Landing Zone*** dans le Cloud repose sur 4 familles de principes, d'outils et/ou de bonnes pratiques.
Nous parlons avant tout ici de principes d'architectures Cloud (**1**) et d'éléments de connectivité (**2**) depuis et vers le Cloud, le réseau WAN du SI et Internet. Tout cela devant être conçu, developpé, testé, intégré et déployé à l'aide d'une plateforme CICD (***3***) permettant d'appliquer les méthodologies ***agiles***.

Bien sûr, l'agilité ne signifie en rien l'absence d'une gouvernance (***4***) adaptée, qui est le facteur clef de la réussite de l'utilisation du Cloud pour la transformation du SI d'Entreprise et de son mantien en condition opérationnelle.

### Explications détaillées

|#|Family|Item|Description|
|-|------|----|-----------|
|||||
|1|Architecture|Cloud Native|L'expression ***Cloud Native*** désigne une architecture spécifiquement développée pour utiliser de façon optimale le Cloud afin de bénéficer de ses capacités de résilience et de performances en réduisant autant que possible ses coûts de fonctionnement en fonction du besoin.|
|||Scalability|La ***scalability*** (ou élasticité en français) est la capacité qu'un système a de se redimensionner (croissance ou décroissance) en fonction de son utilisation (ou de sa charge).|
|||Resilience| La ***résilience*** est une caractéristique qui fait partie du concept ***Cloud Native*** mais dont l'importance mérite d'être spécifiquement rappelée. Elle représente la capacité qu'un système a de continuer de fonctionner en cas de panne d'un ou de plusieurs de ses composants, et ceci sans perte de niveau de service.|
|||Self Healing|Le ***self healing*** (auto-guérison) est la capacité qu'un système a de se réparer lui-même en cas d'une panne d'un de ses composants.|
|||||
|||||
|2|Connectivity|Network|Le ***Network*** est l'infrastructure réseau en place dans le Cloud (dans l'immense majorité des cas avec des IP respectant la [RFC 1918](https://datatracker.ietf.org/doc/html/rfc1918)).|
|||Private Link|Un ***Private Link*** est principalement, soit un tunnel VPN (via Internet), soit une liaision spécialisée (Leased Line via un opérateur), pour relier le réseau WAN de l'Entreprise avec le réseau privé construit dans le Cloud.|
|||Outbound Flows|Les ***Outbound Flows*** sont les flux (techniques) sortants depuis une infrastructure Cloud, soit vers Internet, soit vers le WAN (via le Private Link) de l'Entreprise ou vers une autre infrastructure Cloud. Ils doivent être connus et doivent respecter les directives de sécurité prélablement définies.|
|||Inbound|Les ***Inbound Flows*** sont les flux (techniques) entrants vers une infrastructure Cloud depuis Internet, depuis le WAN (Via le Private Link) de l'Entreprise ou depuis une autre infrastructure Cloud. Ils doivent être connus et doivent respecter les directives de sécurité prélablement définies. |
|||||
|||||
|3|CICD Platform|Agile Software Management|Le choix d'un logiciel de gestion de développement est important et dépend notamment de la méthodologie agile que l'on souhaite appliquer mais aussi en fonction du (ou des) Cloud Prodiver(s) choisi(s). Une solution SaaS est intéressante pour éviter d'avoir un produit supplémentaire à maitenir. À définir en fonction du besoin et de la politique de l'Entreprise sur la localisation des données.|
|||Sources Repository|Je pense que s'il n'est plus nécessaire de présenter l'intérêt de l'utilisation d'un outil de gestion de versions du Code Source, il est toutefois important de définir une méthodologie d'utilisation pour en tirer pleinement partie. Il existe de nombreuses méthodes et standards à ce sujet. Il faut choisir ceux adaptés à sa façon de travailler et au nombre d'équipes de développement.|
|||Pipelines|L'industrialisation du cycle de développement (agile) d'un produit (ou logiciel) est aujourd'hui complètement rentré dans les standards. Si la partie déploiement (***C***ontinuous ***D***elivery/Deployment) est relativement bien maitrisée, il reste encore un peu de chemin à parcourir sur l'aspect intégration (***C***ontinuous ***I***ntegration). Les tests restent le parent pauvre du ***CI/CD*** et notamment les méthodologies de développement liées aux tests (TDD/***T***ests ***D***riven ***D***evelopments).|
|||Artifact Respository|Un ***Artifact Respository*** est le pendant du ***Source Repository*** pour les productions ***d'objets binaires*** (ou simplement ***binaires***) associés à des métadonnées (dont le numéro de version). Il référence aussi les dépendances entre les ***binaires*** produits et les ***binaires*** nécessaires à leur production (build). L'un des grands souhaits de nos RSSI est de s'assurer que les ***binaires*** utilisés dans nos applications soient issues de l'***Articfact Respository*** de l'Entreprise afin de maitriser la sécurité du parc applicatif.|
|||||
|||||
|4|Governance|Docs & Standards|La documentation est un élément incontournable pour appréhender un système complexe. Elle doit être adaptée sur le fond et sur la forme à ceux qui en ont besoin. Elle doit être à jour et les éléments qui la composent doivent être relativement génériques pour le garantir. Tout comme n'importe quel code source, la documentation doit être versionnée et donc intégrée si possible dans un ***Source Respository***.  Les standards représentent un élément clef de la définition et de la réutilisation de ***composants*** et garantissent la simplicité et la stabilité d'un système ainsi que sa mise à jour. Il faut aussi savoir les remettre en question lorsque le besoin le nécessite.|
|||IAM|La mise en place d'un outil de gestion des identités et des accès est un élément incontournable. Selon les cas, il est souvent nécessaire de bien différencier les identités et les accès relatifs à l'utilisation d'une application, de ceux relatifs à sa construction. Il peut être nécessaire d'avoir deux IAM : Un technique (pour la construction) et un fonctionnel (pour l'utilisation). Un administrateur ne devrait pas se servir de la même identité pour utiliser son poste de travail (les applications d'Entreprise, sa messagerie ou Internet) que celle qu'il utilise pour manipuler les éléments techniques du SI d'Entreprise.|
|||Dashboards|Les éléments de type tableau de bord doivent être générés automatiquement pour être le reflet de ce qui existe ou de son évolution.|
|||Monitoring / Alerting|Mettre en place un système de supervision et d'alerte permettant de connaitre à chaque instant l'état de santé du Système d'Information est essentiel. La supervision doit aussi permettre l'analyse post-mortem des incidents. Elle doit être la plus précise possible et la rétention des données qui la composent, adaptée au besoin. Les alertes ne doivent être générées que lors d'une absolue nécessité. Dans le cas contraire, un simple évènement, que l'on pourra traiter en temps voulu, fera tout à fait l'affaire. C'est primordial pour faire confiance à son système de supervision. |
|||Security Management|Le management de la sécurité doit permettre d'interdire ou de remonter les infractions aux directives de sécurité établies par la ***PSSI*** (**P**olitique de **S**écurité du **S**ystème d'**I**nformation). La sécurité ne doit pas être une contrainte, elle est nécessaire pour protéger la valeur générée par l'Entreprise. Les Clouds disposent actuellement d'outils permettant d'appliquer ces directives. Des produits tiers sont proposés sur le marché pour compléter cette offre et permettre d'avoir une vision multi-cloud de la sécurité de son SI. |
|||Cost Management|Le Cloud apporte une nouvelle façon d'appréhender les coûts. Ceux-ci représentent essentiellement des coûts de fonctionnement (OPEX) et doivent être constamment supervisés. Le mode de paiment à l'utilisation (**P**ay **A**s **Y**ou **G**o) nécessite un changement de comportement sur l'utilisation des environnements de POC (**P**roof **O**f **C**oncept), de développement (supprimer ou *éteindre* une infrastructure inutilisée par exemple) ou de production (utilisation de l'élasticité). Ensuite, une mauvaise utilisation ou méconnaissance d'un composant peut rapidement engendrer des coûts non prévus. Les Cloud Providers changent aussi régulièrement de modèle de facturation et il est donc nécessaire de mesurer rapidement ces changements de coûts pour adapter les infrastructures qui les génèrent. De plus, il existe des réductions de coûts proposés par ces derniers qui permettent, si elles sont bien utilisées, de faire des économies substentielles. Le Cloud a fait apparaitre un nouveau métier : FinOps. Les architectes doivent mettre en place les outils permettant aux FinOps de maitriser tout cela.|
|||Inventory Management|Gérer les assets informatiques de l'Entreprise est toujours utile mais les outils doivent être adaptés à cette nouvelle façon de consommer dans le Cloud.|
|||Update Management|Pour garantir une dette technologique la plus basse possible, la mise à jour des infrastructures Cloud doivent se faire en respectant les principes de construction (***Cloud Native***). Il est nécessaire de revoir sa façon de procéder mais il est toujours important de connaitre l'état de son SI pour maitriser sa sécurité et son maintien en condition opérationnelle.|
|||Change Management|Le ***Change Management*** reste bien évidemment d'actualité, mais son mode de fonctionnement doit être forcément repensé et adapté aux nouvelles possibilités du Cloud et à l'utilisation des méthodes agiles. Certaines entreprises font une mise en production de certaines applications toutes les 15 min pour faire face à des besoins clients évoluant en temps réel et ne pas perdre de parts de marché. Les processus de Change Management doivent donc être adaptés pour répondre à ce type de besoin. Il faut garder à l'esprit les objectifs (mesure d'impact, communication, traçabilité, ...) de ceux-ci afin d'y répondre autrement.|

## Liens sur les Landing Zones (ou Cloud Foundation) chez les Cloud Providers Azure, GCP et AWS

Le tableau, ci-dessous, présente quelques liens relatifs à la définition d'une Landing Zone (ou Cloud Foundation) des Clouds Azure, GCP et AWS.

De façon plus large, certains de ces liens présentent aussi les principes et les bonnes pratiques proposés par les Cloud Providers.

|Cloud Providers|Liens|Commentaires|
|---------------|-----|------------|
|Azure|[Microsoft Cloud Adoption Framework for Azure](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/)|Documentations, bonnes pratiques et outils conseillés pour une meilleure adoption du Cloud Azure.|
||[Azure Landing Zone](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/)|La définition de la ***Landing Zone*** selon Azure.|
|GCP|[Best Practices for enterprise organisation](https://cloud.google.com/docs/enterprise/best-practices-for-enterprise-organizations)||
||[Google Cloud Architecture Framework](https://cloud.google.com/architecture/framework)|Guide des bonnes pratiques à suivre pour aider les entreprises à comprendre et utiliser le Cloud GCP en fonction de leurs besoins.|
||[Cloud Foundation Toolkit](https://cloud.google.com/foundation-toolkit)|Toolkit (modèles techniques) proposé par Google aux entreprises pour accélérer l'utilisation du Cloud GCP.|
|AWS|[AWS Landing Zone](https://aws.amazon.com/solutions/implementations/aws-landing-zone/?nc1=h_ls)|AWS Landing Zone permet d'aider les entreprises à configurer plus rapidement un environnement AWS multi-comptes en utilisant les bonnes pratiques.|
