---

copyright:
  years: 2016, 2017
lastupdated: "2016-04-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Génération de projets de cloud natifs
{: #web-mobile}

Vous pouvez gérer des applications de cloud natives via le concept des [projets](projects.html) {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}. La création d'un projet est possible en utilisant la console [{{site.data.keyword.dev_console}}](devex.html) ou le plug-in  [{{site.data.keyword.dev_cli_notm}}](dev_cli.html) pour l'interface de ligne de commande {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}. La console {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} regroupe les fonctionnalités de service les plus courantes nécessaires à un développeur d'applications de cloud natives, dans un endroit unique et connecté, qui a été optimisé pour ce développeur.

La console {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} permet à un développeur d'applications de cloud natives de créer un projet à partir de différents [types de modèle](patterns.html) et [modules de démarrage](starters.html), de créer et de connecter des services clé {{site.data.keyword.Bluemix_notm}} optimisés dans votre projet et de télécharger rapidement du code d'exécution avec des SDK. Ces derniers sont complètement intégrés avec des données d'identification de fonctionnalités ou des dépendances qui vous permettent  d'activer la fonction correspondante sur votre périphérique en quelques minutes. Quand votre application s'exécute et que vous avez défini et configuré les fonctionnalités, vous pouvez revenir à votre projet pour surveiller et gérer l'engagement des utilisateurs de l'application. Vous pouvez aussi configurer et gérer vos services via la console {{site.data.keyword.dev_console}}.

<!--
While the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} provides an integrated development experience, some developers might still want to have finer-grained control and wire services together manually. If this is your preferred approach, you might want to consider using the [{{site.data.keyword.mobilefirstbp}} Starter boilerplate](try_mobile.html).
-->

<!--With {{site.data.keyword.Bluemix}} Mobile services, you can incorporate pre-built, managed, and scalable cloud services into your mobile applications. You can focus on building your mobile apps, instead of the complexities of managing the back-end infrastructure.

The Mobile dashboard provides an integrated experience on {{site.data.keyword.Bluemix_notm}} where you can create mobile projects easily from within the dashboard.
-->


## Projets
{: #projects}

La console {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} combine l'interface utilisateur, les données et les services d'une application au sein d'un *projet* complet. Lorsque vous créez un projet, tous les composants requis de votre application, ainsi que les fonctions ajoutées sont gérées sur le serveur {{site.data.keyword.Bluemix_notm}}. Vous pouvez télécharger le code de votre application ainsi que les données d'identification et les initialiseurs requis si les services sont configurés dans votre projet. Vous pouvez afficher tous vos projets en sélectionnant **Projets**.  

Vous pouvez afficher des informations supplémentaires sur un projet unique en le sélectionnant dans la page **Projets**. La page relative à la présentation du projet qui s'affiche comprend les services configurés et disponibles pour le projet. Les services sont des fonctions distinctes qui étendent la fonctionnalité de votre application. Etant donné qu'il s'agit d'un ajout individuel, vous pouvez ajouter les services dont vous avez besoin, comme les services de notifications push, d'authentification, de données et de stockage ou d'autres services. Quand vous ajoutez un service à votre projet sur la page relative à la présentation du projet puis suivez les instructions pour le configurer, il est automatiquement associé à votre application. Pour
plus d'informations sur la page Présentation du projet, voir [Page présentation du projet](project_overview_page.html).

Pour créer votre projet, vous devez sélectionner un [modèle](patterns.html) puis un [module de démarrage](starters.html).


### Page de présentation du projet
{: #project_overview}

Vous pouvez afficher et utiliser un seul projet {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} en sélectionnant ce projet sur la page **Projets**, ce qui ouvre la page relative à la présentation du projet. 
{: shortdesc}

La page relative à la présentation du projet affiche une vignette pour chaque fonctionnalité qui est configurée ou disponible pour configuration avec le projet sélectionné. La vignette, qui indique le type de fonctionnalité, comporte un bouton *actions* avec trois boutons verticaux. Les fonctionnalités disponibles incluent, par exemple, les services {{site.data.keyword.mobilepushshort}}, Analytics ou Data et Storage. Les fonctionnalités compatibles dépendant du type de projet et des fonctionnalités disponibles dans la région concernée, il est possible que toutes les fonctionnalités ne soient pas disponibles avec tous les projets. 

Quand un type de fonctionnalité n'est pas encore associé au projet, un bouton **Créer**  est affiché sur la vignette. Les options du bouton
d'actions permettent de créer une instance du service ou d'ajouter une instance de service existante si la fonctionnalité n'est pas encore associée. La sélection de l'option d'ajout d'une instance de service existante fournit une liste des instances de service de ce type au sein de votre espace.

Si la fonctionnalité est déjà associée à ce projet, le nom de l'instance de service associée est affiché sur la vignette après le type de
fonctionnalité, ce qui facilite l'identification de l'instance de service associée à votre projet sur votre console {{site.data.keyword.dev_console}}. Les
actions disponibles sur le bouton d'action sont les suivantes : **Afficher** et **Retirer** quand la fonctionnalité est déjà associée au projet. Le retrait d'une instance de service efface seulement l'association à ce projet et ne supprime pas l'instance de service de votre console {{site.data.keyword.dev_console}}. Pour supprimer une instance de service, cliquez sur la page accessible en sélectionnant les options relatives aux services Web et mobiles pour afficher et supprimer les instances de service voulues.

Sélectionnez la commande relative à l'obtention du code sur la vignette **Code** pour télécharger le code pour votre projet. Pour plus d'informations sur le
téléchargement du code, voir [Obtention du code](get_code.html).


### Mise à jour de votre projet pour utiliser un nouveau module de démarrage
{: #update-starter}

1. Depuis la page relative aux projets ou à la présentation du projet, cliquez sur l'icône du menu déroulant dynamique et sélectionnez le module de démarrage de la mise à jour.

2. Choisissez un nouveau module de démarrage puis cliquez sur **Mettre à jour**.

3. Cliquez sur  la commande relative à l'obtention du code sur la page de présentation du projet pour sélectionner votre langue.

   Vous pouvez également cliquer sur la page **Code**.


### Mise à jour de votre projet pour générer un nouveau langage
{: #update-language}

1. Depuis la page relative au projet ou à la présentation du projet, cliquez sur l'icône du menu déroulant dynamique et sélectionnez le module de démarrage de la mise à jour.

2. Sélectionnez un nouveau langage et cliquez sur **Mettre à jour**.

3. Cliquez sur  la commande relative à l'obtention du code sur la page de présentation du projet pour sélectionner votre langue.


## Types de modèle
{: #patterns}

Les modèles de cloud natifs sont des structures qui ont fait leur preuve et dont l'utilisation permet de garantir une topologie fiable, évolutive et cohérente pour vos applications. Quand vous créez un projet, il vous est proposé différents types de modèle parmi lesquels vous pouvez choisir. Vous sélectionnez simplement le type de modèle et les fonctionnalités que vous voulez incorporer dans votre projet. Une fois vos préférences de projet définies, un projet de démarrage est généré que vous pouvez éditer, exécuter ou déboguer, et déployer localement ou dans {{site.data.keyword.Bluemix}}.


### Application Web
{: #web}

Les projets Web donnent la possibilité de servir du contenu Web (HTML, JavaScript et feuilles de style, par exemple) sur le serveur Web.

Les modules de démarrage Web suivants sont disponibles :

* Basic Web : sert un fichier `index.html` statique, une feuille de style vide et par défaut et un fichier JavaScript.
* Webpack : crée un projet dans lequel les fichiers source ES6 (ECMAScript 6) se trouvent dans `src/client` et sont compilés avec WebPack, pour en retirer les caractères non essentiels, puis convertis pour utilisation dans le navigateur.
* Webpack + React : infrastructure riche pour générer des interfaces utilisateur. Les fichiers source, qui se trouvent dans `src/client/app`, seront compilés avec WebPack et servis dans l'annuaire public.


### Application mobile
{: #mobile}

Les modèles d'application mobile vous aident à gérer des applications mobiles qui se connectent directement aux services de backend, comme {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}},
{{site.data.keyword.appid_short}}, etc. Des projets peuvent également être ajoutés via sdkGen, comme BFF, et Microservices.

Vous pouvez choisir dans une liste de modules de démarrage, comme {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}}, etc.

Vous pouvez générer des applications mobiles dans Swift, Android ou Cordova.


### BFF (Backend for Frontend)
{: #bff}

Les modèles BFF vous permettent de vous concentrer efficacement sur l'exposition des données et services métier sous une forme qui répond aux besoins d'interaction de l'utilisateur. Pour optimiser la démarche utilisateur vers votre solution de cloud, il peut s'avérer nécessaire de mettre en place une démarche utilisateur différente pour l'application mobile et une démarche plus détaillée et plus riche pour l'application Web. Avec l'introduction de périphériques pilotés par la voix comme le service [{{site.data.keyword.conversationfull}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/conversation.html), l'interaction avec l'utilisateur peut être contrôlée par la voix. Ce canal numérique nécessite une architecture BFF très différente pour gérer ces interactions vocales.

Avec {{site.data.keyword.Bluemix_notm}}, vous pouvez générer une architecture BFF en mettant en oeuvre une approche de programmation polyglotte pour procéder à sa définition. IBM recommande d'utiliser Node.js, Swift ou Java, en les exécutant dans un environnement de cloud natif, avec les services Cloud Foundry, Container ou sans serveur.

L'architecture BFF gère l'intégration avec les services pour la persistance des données, la mise en cache et l'intégration à des services à haute valeur comme {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, et l'analyse de données, tel {{site.data.keyword.sparks}}.

L'architecture BFF expose une API se servant le plus souvent d'un modèle REST mais vous pouvez concevoir votre architecture BFF afin qu'elle fonctionne depuis une architecture de messagerie utilisant {{site.data.keyword.messagehub}}.

Un module de démarrage BFF Basic est disponible via Node.js ou Swift.


### Microservice
{: #microservice}

Les projets Microservice constituent le fondement de la génération de microservices de backend, incluant un noeud final de santé de base, une API REST. Les projets générés contiendront toutes les dépendances requises pour les microservices eux-mêmes ainsi que pour tout service de cloud attaché.

Un module de démarrage Microservice Basic est disponible en utilisant Java.

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


### Langages
{: #languages notoc}

Les langages pris en charge sont :

   * [Java ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](../runtimes/swift/getting-started.html){: new_window}


#### Java
{: #java notoc}

Java dispose de fonctionnalités qui ont fait leur preuve pour générer des applications destinées aux entreprises, mais les nouvelles fonctionnalités de Java 8, associées à des temps d'exécution de poids plus réduit comme ceux assurés par Liberty et les infrastructures telles Spring Boot, font de Java un outil également parfaitement adapté à la génération des microservices.


#### Node.js
{: #node notoc}

Node.js est un environnement d'exécution JavaScript qui utilise un modèle d'entrée/sortie non bloquant, géré par événement, qui le rend léger, efficace et extrêmement performant au niveau de la capacité de traitement et de l'évolutivité pour les applications Web, les modèles BFF et les microservices. L'écosystème de package Node.js, npm, permet d'accéder à une large collection de modules open source, fournissant une large gamme de fonctionnalités pour accélérer le développement de votre application.


#### Swift
{: #swift notoc}

Swift est un langage de programmation moderne créé par Apple en 2014 qui a été conçu pour remplacer Objective C, en open source, en décembre 2015. Il sert aujourd'hui à générer iOS, macOS, des services Web et des logiciels système sous les systèmes d'exploitation Linux et macOS via l'architecture x86, ARM ou Z. Il écrit comme un langage de script mais est compilé pour obtenir des performances élevées similaires à C avec de faibles temps de traitement, ce qui le rend idéal pour les environnements d'exécution de cloud. Il se sert d'un système de type statique et fort que vous retrouvez dans Java alors que le style fonctionnel et les routines asynchrones correspondent à ce que vous voyez dans JavaScript. Swift est donc très performant, la source compile en code natif en utilisant la chaîne d'outils du compilateur LLVM et il est capable d'optimiser facilement des bibliothèques de systèmes externes écrites en C.


## Modules de démarrage
{: #starters}

Avec la console {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}, vous pouvez choisir parmi différents modules de démarrage pour chaque type de modèle.

Les modules de démarrage sont optimisés pour constituer du code de démarrage prêt pour la production présentant une intégration {{site.data.keyword.Bluemix_notm}} clé avec un service à valeur élevée. Chaque module de démarrage se concentre sur un service et illustre
l'intégration des logiciels SDK de ce service dans le code. Dans certains cas,
les modules de démarrage proposent une expérience
utilisateur simple qui met en évidence l'intégration des données du service ou les
interactions avec l'utilisateur. Chaque module de démarrage est configuré pour être activé avec les services d'authentification ou de données et éventuellement d'autres fonctionnalités, si vous décidez de les configurer pour votre projet.
