
---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Types de modèle
{: #patterns}

Les modèles de cloud natifs sont des structures qui ont fait leur preuve et dont l'utilisation permet de garantir une topologie fiable, évolutive et cohérente pour vos applications. Quand vous créez un projet, il vous est proposé différents types de modèle parmi lesquels vous pouvez choisir. Vous sélectionnez simplement le type de modèle et les fonctionnalités que vous voulez incorporer dans votre projet. Une fois vos préférences de projet définies, un projet de démarrage est généré que vous pouvez éditer, exécuter ou déboguer, et déployer localement ou dans {{site.data.keyword.Bluemix}}.

## Application Web
{: #web}

Les projets Web donnent la possibilité de servir du contenu Web (HTML, JavaScript et feuilles de style, par exemple) sur le serveur Web.

Les modules de démarrage Web suivants sont disponibles :

* Basic Web : sert un fichier `index.html` statique, une feuille de style vide et par défaut et un fichier JavaScript.
* Webpack : crée un projet dans lequel les fichiers source ES6 (ECMAScript 6) se trouvent dans `src/client` et sont compilés avec WebPack, pour en retirer les caractères non essentiels, puis convertis pour utilisation dans le navigateur.
* Webpack + React : infrastructure riche pour générer des interfaces utilisateur. Les fichiers source, qui se trouvent dans `src/client/app`, seront compilés avec WebPack et servis dans l'annuaire public.


## Application mobile
{: #mobile}

Les modèles d'application mobile vous aident à gérer des applications mobiles qui se connectent directement aux services de backend, comme {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}},
{{site.data.keyword.appid_short}}, etc. Des projets peuvent également être ajoutés via sdkGen, comme BFF, et Microservices.

Vous pouvez choisir dans une liste de modules de démarrage, comme {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}}, etc.

Vous pouvez générer des applications mobiles dans Swift, Android ou Cordova.


## BFF (Backend for Frontend)
{: #bff}

Les modèles BFF vous permettent de vous concentrer efficacement sur l'exposition des données et services métier sous une forme qui répond aux besoins d'interaction de l'utilisateur. Pour optimiser la démarche utilisateur vers votre solution de cloud, il peut s'avérer nécessaire de mettre en place une démarche utilisateur différente pour l'application mobile et une démarche plus détaillée et plus riche pour l'application Web. Avec l'introduction de périphériques pilotés par la voix comme le service [{{site.data.keyword.conversationfull}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/conversation.html), l'interaction avec l'utilisateur peut être contrôlée par la voix. Ce canal numérique nécessite une architecture BFF très différente pour gérer ces interactions vocales.

Avec {{site.data.keyword.Bluemix_notm}}, vous pouvez générer une architecture BFF en mettant en oeuvre une approche de programmation polyglotte pour procéder à sa définition. IBM recommande d'utiliser Node.js, Swift ou Java, en les exécutant dans un environnement de cloud natif, avec les services Cloud Foundry, Container ou sans serveur.

L'architecture BFF gère l'intégration avec les services pour la persistance des données, la mise en cache et l'intégration à des services à haute valeur comme {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, et l'analyse de données, tel {{site.data.keyword.sparks}}.

L'architecture BFF expose une API se servant le plus souvent d'un modèle REST mais vous pouvez concevoir votre architecture BFF afin qu'elle fonctionne depuis une architecture de messagerie utilisant {{site.data.keyword.messagehub}}.

Un module de démarrage BFF Basic est disponible via Node.js ou Swift.


## Microservice
{: #microservice}

Les projets Microservice constituent le fondement de la génération de microservices de backend, incluant un noeud final de santé de base, une API REST. Les projets générés contiendront toutes les dépendances requises pour les microservices eux-mêmes ainsi que pour tout service de cloud attaché.

Un module de démarrage Microservice Basic est disponible en utilisant Java.

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


## Langages
{: #languages notoc}

Les langages pris en charge sont :

   * [Java ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](../runtimes/swift/getting-started.html){: new_window}


### Java
{: #java notoc}

Java dispose de fonctionnalités qui ont fait leur preuve pour générer des applications destinées aux entreprises, mais les nouvelles fonctionnalités de Java 8, associées à des temps d'exécution de poids plus réduit comme ceux assurés par Liberty et les infrastructures telles Spring Boot, font de Java un outil également parfaitement adapté à la génération des microservices.


### Node.js
{: #node notoc}

Node.js est un environnement d'exécution JavaScript qui utilise un modèle d'entrée/sortie non bloquant, géré par événement, qui le rend léger, efficace et extrêmement performant au niveau de la capacité de traitement et de l'évolutivité pour les applications Web, les modèles BFF et les microservices. L'écosystème de package Node.js, npm, permet d'accéder à une large collection de modules open source, fournissant une large gamme de fonctionnalités pour accélérer le développement de votre application.


### Swift
{: #swift notoc}

Swift est un langage de programmation moderne créé par Apple en 2014 qui a été conçu pour remplacer Objective C, en open source, en décembre 2015. Il sert aujourd'hui à générer iOS, macOS, des services Web et des logiciels système sous les systèmes d'exploitation Linux et macOS via l'architecture x86, ARM ou Z. Il écrit comme un langage de script mais est compilé pour obtenir des performances élevées similaires à C avec de faibles temps de traitement, ce qui le rend idéal pour les environnements d'exécution de cloud. Il se sert d'un système de type statique et fort que vous retrouvez dans Java alors que le style fonctionnel et les routines asynchrones correspondent à ce que vous voyez dans JavaScript. Swift est donc très performant, la source compile en code natif en utilisant la chaîne d'outils du compilateur LLVM et il est capable d'optimiser facilement des bibliothèques de systèmes externes écrites en C.
