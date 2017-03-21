---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Scénarios d'utilisation {{site.data.keyword.openwhisk_short}} courants
{: #openwhisk_common_use_cases}

Le modèle d'exécution proposé par {{site.data.keyword.openwhisk_short}} prend en charge divers scénarios d'utilisation. Les sections ci-après présentent des exemples classiques. Pour obtenir une présentation plus détaillée de l'architecture sans serveur, voir l'excellent [article de Mike Roberts sur le blogue de Martin Fowler](https://martinfowler.com/articles/serverless.html) qui contient des scénarios d'utilisation et présente les avantages et les inconvénients et les meilleures pratiques d'implémentation de cette architecture.
{: shortdesc}

## Microservices
{: #openwhisk_common_use_cases_microservices}

En dépit des avantages qu'elles procurent, les solutions basées sur les microservices sont toujours aussi difficiles à générer à l'aide de technologies cloud traditionnelles nécessitant souvent de contrôler une chaîne d'outils complexe et d'avoir recours à des pipelines de génération et d'opérations distincts. Les équipes réduites mais agiles, qui consacrent trop de temps à gérer les complexités d'infrastructure et de fonctionnement (tolérance aux pannes, équilibrage de charge, mise à l'échelle automatique et journalisation), souhaitent plus précisément pouvoir développer un code simplifié à valeur ajoutée à l'aide de langages de programmation qu'ils connaissent et apprécient et qui conviennent mieux pour la résolution de problèmes spécifiques.  

La nature modulaire et intrinsèquement évolutive d'{{site.data.keyword.openwhisk_short}} en fait un service idéal pour l'implémentation d'éléments de logique granulaires dans les actions. Les actions {{site.data.keyword.openwhisk_short}} sont indépendantes les unes des autres et peuvent être implémentées à l'aide d'une grande variété de langages pris en charge par {{site.data.keyword.openwhisk_short}} et accèdent à différents systèmes de back end. Chaque action peut être déployée, gérée et mise à l'échelle indépendamment des autres actions. L'interconnectivité entre les actions est fournie par {{site.data.keyword.openwhisk_short}} sous forme de règles, de séquences et de conventions de dénomination. Ce qui est de bon augure pour les applications basées sur les microservices. 

## Applications Web
{: #openwhisk_common_use_cases_webapps}

{{site.data.keyword.openwhisk_short}} a été conçu pour la programmation basée sur des événements, cependant, il offre plusieurs avantages pour les applications utilisées par les utilisateurs. Par exemple, lorsque vous l'associez à un petit module de remplacement Node.js, vous pouvez l'utiliser pour servir des applications plutôt faciles à déboguer. De plus, étant donné que les applications {{site.data.keyword.openwhisk_short}} utilisent le processeur de manière beaucoup moins intensive que lorsqu'un processus serveur est exécuté sur une plateforme sous forme de service, elles coûtent beaucoup moins cher.  

Une application Web complète peut être construite et exécutée avec OpenWhisk. Le fait de combiner des API sans serveur avec un hébergement de fichier statique pour des ressources de site, c'est-à-dire, des ressources HTML, JavaScript et CSS, signifie que nous pouvons construire des applications Web sans serveur entières. La simplicité de l'exploitation d'un environnement {{site.data.keyword.openwhisk_short}} hébergé (ou le fait de ne pas avoir à exécuter quoi que ce soit dans la mesure où il est hébergé sur Bluemix) est sans commune mesure avec la mise en oeuvre et l'exploitation d'un serveur Node.js Express ou tout autre contexte d'exécution de serveur traditionnel. 

L'option "--annotation web-export true" de l'outil *wsk*, utilisable via l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}}, est également très appréciable car elle permet d'accéder au code à partir d'un navigateur Web. 

Voici quelques exemples d'utilisation d'{{site.data.keyword.openwhisk_short}} pour construire une application Web :
- [Web Actions: Serverless Web Apps with OpenWhisk](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba).
- [Build a user-facing {{site.data.keyword.openwhisk_short}} application with Bluemix and Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverless HTTP handlers with OpenWhisk](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

Même s'il est tout à fait possible d'implémenter des applications IoT à l'aide d'architectures de serveur traditionnelles, il n'en reste pas moins que dans de nombreux cas, la combinaison de différents services et ponts de données nécessite des pipelines extrêmement performants et flexibles, allant des périphériques IoT au stockage en cloud et à une plateforme d'analyse. Souvent les ponts préconfigurés ne disposent pas de la programmabilité requise pour implémenter et ajuster une solution d'architecture spécifique. Etant donné la grande variété de pipelines possibles et le manque de standardisation en matière de fusion des données en général et pour IoT en particulier, le pipeline nécessite très souvent une transformation des données personnalisées (pour la conversion de format, le filtrage, l'augmentation, etc.). {{site.data.keyword.openwhisk_short}} est un outil idéal pour implémenter ce type de transformation selon une méthode 'sans serveur' où la logique personnalisée est hébergée sur une plateforme cloud élastique et entièrement gérée. 

Souvent, les scénarios Internet of Things dépendent intrinsèquement d'un capteur. Par exemple, une action dans {{site.data.keyword.openwhisk_short}} peut être déclenchée s'il est nécessaire de réagir à un relevé de capteur dépassant une température particulière. Les interactions IoT sont généralement sans état avec un niveau de charge potentiellement très élevé dans le cas d'événements majeurs (catastrophes naturelles, événements climatiques extrêmes, embouteillages, etc.). Ces situations nécessitent un système élastique qui doit pouvoir être capable de passer rapidement d'une charge de travail normale faible à une charge de travail beaucoup plus élevée avec des temps de réponse prévisibles et être capable de traiter un nombre d'événements extrêmement élevé sans avertissement préalable. Il est très compliqué de créer un système répondant à ces exigences à l'aide d'architectures de serveur traditionnelles car ces dernières ont tendance soit à manquer de puissance et à être incapables de prendre en charge des hausses de trafic soit à être approvisionnées de manière excessive et à être extrêmement réactives. 

Voici un exemple d'application IoT qui utilise OpenWhisk, NodeRed, Cognitive et d'autres services : [Serverless transformation of IoT data-in-motion with OpenWhisk](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt).

![Exemple d'architecture de solution IoT](images/IoT_solution_architecture_example.png)

## Système de back end d'API
{: #openwhisk_common_use_cases_iot}

Les plateformes informatiques sans serveur permettent aux développeurs de créer rapidement des API sans utiliser de serveurs. {{site.data.keyword.openwhisk_short}} prend en charge la génération automatique d'API REST pour des actions et vous pouvez rapidement rapidement l'outil de gestion d'API de votre choix (par exemple, [IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) ou autre) aux API REST fournies par OpenWhisk. A l'instar d'autres scénarios d'utilisation, toutes les remarques concernant l'évolutivité et d'autres qualités de service s'appliquent.  

Voici un exemple et une discussion concernant l'[utilisation d'une plateforme sans serveur en tant que système de back end d'API](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples).

## Système de back end mobile
{: #openwhisk_common_use_cases_mobile}

De nombreuses applications mobiles requièrent une logique côté serveur. Pour les développeurs d'applications mobiles qui ne souhaitent pas gérer une logique côté serveur et préfèrent se concentrer sur l'application qui s'exécute sur le périphérique ou le navigateur, l'utilisation d'{{site.data.keyword.openwhisk_short}} comme système de back end côté serveur est la solution. De plus, la prise en charge intégrée de Swift permet aux développeurs de réutiliser leurs compétences en programmation iOS. Les applications mobiles présentent souvent des modèles de charge imprévisibles et une solution hébergée par {{site.data.keyword.openwhisk_short}}, telle qu'IBM Bluemix, est capable d'évoluer afin de répondre à pratiquement n'importe quelle demande en matière de charge de travail sans avoir à fournir des ressources à l'avance. 

## Traitement de données
{: #openwhisk_common_use_cases_data}

Etant donné la quantité de données désormais disponible, le développement d'applications doit pouvoir traiter de nouvelles données, et éventuellement y réagir. Cette exigence inclut le traitement d'enregistrements de base de données structurés ainsi que de vidéos, d'images ou de documents non structurés. {{site.data.keyword.openwhisk_short}} peut être configuré via des flux fournis par le système ou personnalisés afin de réagir aux changements de données et d'exécuter automatiquement des actions sur les flux de données entrants. Les actions peuvent être programmées pour traiter des modifications, transformer des formats de données, envoyer et recevoir des messages, appeler d'autres actions, mettre à jour différents magasins de données, y compris des bases de données relationnelles SQL, des grilles de données en mémoire, une base de données, des fichiers, des courtiers de messages NoSQL et une variété d'autres systèmes. Les règles et séquences {{site.data.keyword.openwhisk_short}} fournissent suffisamment de souplesse pour modifier le pipeline de traitement sans avoir à effectuer de tâche de programmation, simplement via des changements de configuration. Cela rend le système basé sur {{site.data.keyword.openwhisk_short}} extrêmement agile et facilement adaptable à l'évolution des exigences. 

## Applications cognitives
{: #openwhisk_common_use_cases_cognitive}

Les technologies cognitives peuvent être combinées efficacement avec {{site.data.keyword.openwhisk_short}} pour créer des applications puissantes. Par exemple, IBM Alchemy API et Watson Visual Recognition peuvent être utilisés avec {{site.data.keyword.openwhisk_short}} pour extraire automatiquement des informations utiles provenant de vidéos sans avoir à regarder ces dernières  

Voici un exemple d'application [Dark Vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp) qui permet de faire cela. Dans cette application, l'utilisateur télécharge une vidéo ou une image à l'aide de l'application Web Dark Vision, qui la stocke dans une base de données Cloudant. Une fois la vidéo téléchargée, {{site.data.keyword.openwhisk_short}} la détecte en écoutant les modifications Cloudant (déclencheur). {{site.data.keyword.openwhisk_short}} déclenche ensuite l'action d'extraction de vidéo. Pendant son exécution, l'extracteur produit des images et les stocke dans Cloudant. Les images sont ensuite traitées à l'aide de Watson Visual Recognition et les résultats sont stockés dans la même base de données Cloudant. Les résultats peuvent être affichés à l'aide de l'application Web Dark Vision OU d'une application iOS. Object Storage peut être utilisé en plus de Cloudant. Dans ce cas, les métadonnées de vidéo et d'image sont stockées dans Cloudant et les fichiers de support sont stockés dans Object Storage.
