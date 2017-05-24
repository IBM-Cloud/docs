---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# A propos de Continuous Delivery  
{: #cd_about}  

Avec {{site.data.keyword.contdelivery_full}}, vous pouvez construire, tester et livrer des applications en suivant des pratiques DevOps et en utilisant des outils à la pointe du secteur.
{:shortdesc}

Le service {{site.data.keyword.contdelivery_short}} prend en charge vos flux de travaux DevOps :

 * Vous pouvez créer des [chaînes d'outils](/docs/services/ContinuousDelivery/toolchains_about.html){: new_window} ouvertes DevOps intégrées activant des intégrations d'outils prenant en charge vos tâches de développement, de déploiement et vos opérations.

  Une chaîne d'outils est un ensemble d'outils intégré que vous pouvez utiliser pour développer, construire, déployer et gérer vos applications
en collaborant avec d'autres utilisateurs. Vous pouvez créer des chaînes d'outils incluant des services {{site.data.keyword.Bluemix_notm}}, des outils open source et des outils d'éditeurs tiers tels que GitHub, PagerDuty et Slack qui rendent reproductibles et plus faciles à gérer le développement et les opérations.

 * Distribution continue à l'aide de [pipelines](/docs/services/ContinuousDelivery/pipeline_about.html){: new_window} automatisés.

  Automatisation des générations, des tests unitaires, des déploiements, etc. Générez, testez et déployez de manière reproductible en intervenant le moins possible. Soyez prêt à lancer en production à tout moment.

 * Edition et envoi du code depuis n'importe quel emplacement à l'aide de l'[interface IDE basée sur
le Web](/docs/services/ContinuousDelivery/web_ide.html){: new_window}.

  Création, édition, exécution, débogage et réalisation de tâches de contrôle des sources dans GitHub. Passage transparent de l'édition du code à son déploiement en production.

 * Amélioration de la qualité via [{{site.data.keyword.DRA_short}}](/docs/services/ContinuousDelivery/di_working.html){: new_window}.

  Identifiez les dynamiques opérant dans votre équipe lors du développement et de la distribution du code. Découvrez comment les utilisateurs interagissent avec votre application. Vérifiez les données pour vous aider à gérer les opérations de votre application.


## Disponibilité de la chaîne d'outils sur Bluemix Public et sur Bluemix Dédié
{: #public_and_dedicated}

{{site.data.keyword.Bluemix_notm}} Public est une plateforme de cloud à norme ouverte qui vous permet de construire, d'exécuter et de gérer des applications accessibles par [http://bluemix.net ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}. {{site.data.keyword.Bluemix_notm}} Dédié fournit les fonctionnalités de {{site.data.keyword.Bluemix_notm}} dans un environnement SoftLayer dédié qui établit une connexion sécurisée à la fois à l'environnement {{site.data.keyword.Bluemix_notm}} Public et à votre réseau. L'environnement {{site.data.keyword.Bluemix_notm}} Dédié de votre société peut ne pas contenir les mêmes intégrations d'outils que le site {{site.data.keyword.Bluemix_notm}} Public.

Pour la gestion du code source et le suivi des problèmes, {{site.data.keyword.Bluemix_notm}} Public utilise généralement github.com. {{site.data.keyword.Bluemix_notm}} Dédié peut également utiliser github.com, mais se sert généralement de {{site.data.keyword.ghe_short}}, qui est installé par votre société ou géré par IBM.

{{site.data.keyword.contdelivery_short}} est disponible sur {{site.data.keyword.Bluemix_notm}} Public et {{site.data.keyword.Bluemix_notm}} Dédié. Les chaînes d'outils varient selon que vous utilisez {{site.data.keyword.contdelivery_short}} sur {{site.data.keyword.Bluemix_notm}} Public ou {{site.data.keyword.Bluemix_notm}} Dédié.

**Astuce **: les chaînes d'outils sont hébergées dans la région sud des Etats-Unis. Si votre chaîne d'outils est configurée pour déployer des applications dans une autre
région, elle déploiera quand même les applications dans cette région.

|Chaînes d'outils |{{site.data.keyword.Bluemix_notm}} public	|{{site.data.keyword.Bluemix_notm}} dédié |
|:----------|:------------------------------|:------------------|
|Intégrations d'outils 		|Pour obtenir une liste des intégrations d'outils prises en charge, voir [Configuration d'intégrations d'outils](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}. 		|Les intégrations d'outils disponibles dépendent de la configuration de {{site.data.keyword.contdelivery_short}} dans votre environnement.			|
|Création d'une chaîne d'outils à partir d'un modèle		|Connectez-vous à [{{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://console.ng.bluemix.net/devops){:new_window}.		|Connectez-vous à votre environnement Dédié sur {{site.data.keyword.Bluemix_notm}}.			|
|Création d'une chaîne d'outils à partir d'une application		|L'application est configurée pour la distribution continue depuis un nouveau référentiel GitHub rempli avec le code de démarrage d'application.		|L'application est configurée pour la distribution continue depuis un nouveau référentiel GitHub ou GitHub Enterprise rempli avec le code de démarrage d'application.		|  
|Régions de déploiement du pipeline de distribution		|Toutes les régions {{site.data.keyword.Bluemix_notm}} Public sont disponibles pour des travaux de déploiement Cloud Foundry. 		|La région {{site.data.keyword.Bluemix_notm}} Dédié est disponible. D'autres régions dédiées ou locales au sein du même compte client peuvent également être disponibles en fonction de la configuration de {{site.data.keyword.contdelivery_short}} dans votre environnement spécifique.		|
|Travaux de déploiement du pipeline de distribution		|Tous les [types de travaux](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs) sont disponibles.		|Les types de travaux dépendant de services {{site.data.keyword.Bluemix_notm}} qui ne sont pas installés dans l'environnement dédié risquent de ne pas être disponibles.	Par exemple, les types de travaux de génération et de déploiement de conteneur peuvent ne pas être disponibles dans des environnements qui ne disposent pas du service de conteneur {{site.data.keyword.Bluemix_notm}}.	|
{: caption="Tableau 1. Différences entre les chaînes d'outils sur Bluemix Dédié et Bluemix Public" caption-side="top"}


## Modèles de chaîne d'outils
{: #templates}

Vous pouvez utiliser un modèle comme point de départ pour [créer une chaîne d'outils ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/create){: new_window}. Les modèles de chaîne d'outils incluent des ensembles spécifiques d'intégrations d'outils prenant en charge des tâches de développement, de déploiement et d'opérations.

**Astuce** : L'environnement {{site.data.keyword.Bluemix_notm}} Dédié de votre société peut ne pas contenir les mêmes modèles de chaîne d'outils que le site {{site.data.keyword.Bluemix_notm}} Public. Les modèles de chaîne d'outils qui sont disponibles à la fois sur {{site.data.keyword.Bluemix_notm}} Public et {{site.data.keyword.Bluemix_notm}} Dédié peuvent contenir un ensemble d'intégrations d'outils différent sur {{site.data.keyword.Bluemix_notm}} Dédié.

Certains modèles de chaîne d'outils incluent des intégrations d'outils qui font partie du service {{site.data.keyword.contdelivery_short}}. Si aucune instance de ce service n'existe dans votre organisation, elle est automatiquement ajoutée, sans aucun frais, lorsque vous cliquez sur **Créer**. Pour plus d'informations et pour obtenir les dispositions applicables, consultez le [catalogue Bluemix ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window}.

Les modèles de chaîne d'outils de microservices déploient une application avec les API Catalog et Orders qui sont sauvegardées par un magasin Cloudant. Dans le cadre du déploiement de l'application, une instance de service Cloudant gratuite est créée. Pour plus d'informations et pour obtenir les dispositions applicables, consultez le [catalogue Bluemix ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/){:new_window}.

|Modèle |Description	|
|:----------|:------------------------------|
|[Chaîne d'outils du tutoriel natif pour le cloud Garage Method ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fcloud-native-toolchain-tutorial){:new_window} 		|Cette chaîne d'outils illustre les pratiques DevOps qui sont appliquées dans la méthode Garage. Elle est préconfigurée pour la distribution continue, le contrôle des sources et l'automatisation des tests, ainsi que pour la surveillance et les opérations automatisées. Elle est fournie avec un modèle d'application écrit en Node.js Express 4, que vous pouvez continuer à étendre. 		|
|[Chaîne d'outils de microservices avec {{site.data.keyword.DRA_short}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Ftoolchain-demo){:new_window} 		|Cette chaîne d'outils native pour le cloud permet de construire, à partir d'un exemple, un magasin en ligne comprenant trois microservices : une API Catalog, une API Orders et une interface graphique qui appelle les deux API. Cette chaîne d'outils est préconfigurée pour la distribution continue, le contrôle des sources, les tests fonctionnels, le suivi des problèmes, l'édition en ligne et la notification d'alerte. 		|
|[Chaîne d'outils de microservices avec {{site.data.keyword.DRA_short}} (v2) ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fmicroservices-toolchain-hosted){:new_window} 		|Cette chaîne d'outils native pour le cloud permet de construire, à partir d'un exemple, un magasin en ligne comprenant trois microservices : une API Catalog, une API Orders et une interface graphique qui appelle les deux API. Cette chaîne d'outils est préconfigurée pour la distribution continue, le contrôle des sources, les tests fonctionnels, le suivi des problèmes, l'édition en ligne et la notification d'alerte. 		|
|[Chaîne d'outils de conteneur sécurisé ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsecure-container-toolchain){:new_window} 		|Cette chaîne d'outils vous permet de développer et de déployer une application de conteneur Docker sécurisée. Par défaut, la chaîne d'outils utilise une application exemple Node.js "Hello World", mais vous pouvez vous lier à votre propre référentiel GitHub à la place. La chaîne d'outils est préconfigurée pour la distribution continue avec Vulnerability Advisor, le contrôle des sources, le suivi des problèmes et l'édition en ligne. 		|
|[Chaîne d'outils Cloud Foundry simple![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain){:new_window}		|Cette chaîne d'outils vous permet de développer et de déployer une application Cloud Foundry. Par défaut, cette chaîne d'outils utilise une application exemple Node.js "Hello World", mais vous pouvez vous lier à votre propre référentiel GitHub à la place. La chaîne d'outils est préconfigurée pour la distribution continue, le contrôle des sources, le suivi des problèmes et l'édition en ligne. 		|
|[Chaîne d'outils Cloud Foundry simple (v2) ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain-hosted){:new_window}	|Cette chaîne d'outils vous permet de développer et de déployer une application Cloud Foundry. Par défaut, cette chaîne d'outils clone une application exemple Node.js "Hello World" dans un référentiel Git hébergé par IBM, que vous pouvez ensuite modifier. La chaîne d'outils est préconfigurée pour la distribution continue, le contrôle des sources, le suivi des problèmes et l'édition en ligne. 		|
|[Chaîne d'outils Cloud Foundry simple avec {{site.data.keyword.DRA_short}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdra-toolchain-demo){:new_window}		|Cette chaîne d'outils native pour le cloud vous permet d'utiliser {{site.data.keyword.DRA_short}} pour mettre en place le déploiement d'une application Cloud Foundry simple. Par défaut, cette chaîne d'outils utilise une application météo exemple Node.js, mais vous pouvez vous lier à votre propre référentiel GitHub. 		|
|[Chaîne d'outils de conteneur simple ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-container-toolchain){:new_window}		|Cette chaîne d'outils vous permet de développer et de déployer une application de conteneur Docker. Par défaut, la chaîne d'outils utilise une application exemple Node.js "Hello World", mais vous pouvez vous lier à votre propre référentiel GitHub à la place. La chaîne d'outils est préconfigurée pour la distribution continue, le contrôle des sources, le suivi des problèmes et l'édition en ligne. 		|
|[Delivery Insights avec IBM UrbanCode Deploy ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdeliveryinsights-toolchain){:new_window}		|Cette chaîne d'outils permet de visualiser les mesures de déploiement d'IBM UrbanCode Deploy. Activez cette chaîne d'outils afin qu'elle communique avec IBM UrbanCode Deploy en téléchargeant et en configurant DevOps Connect à partir de la page Settings de {{site.data.keyword.DRA_short}}. 		|
|[Deployment Risk Analytics avec GitHub et Jenkins ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevopsinsights-toolchain){:new_window}		|Cette chaîne d'outils vous permet d'analyser votre processus Jenkins en vue d'une intégration et d'une distribution continues. Vous pouvez configurer le serveur Jenkins pour qu'il envoie des données à {{site.data.keyword.DRA_short}} lorsque les travaux sont exécutés par Jenkins. Vous pouvez également implémenter des seuils de qualité afin de bloquer des déploiements en fonction de règles. Vous pouvez afficher les résultats sur le tableau de bord Deployment Risk de {{site.data.keyword.DRA_short}}. Si vous configurez un référentiel GitHub pour qu'il indique le référentiel source utilisé par Jenkins, la traçabilité des modifications est disponible.  		|
|[Developer Insights et Team Dynamics avec GitHub et JIRA ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevteaminsights-toolchain){:new_window}		|Cette chaîne d'outils vous permet d'explorer les risques liés au développement de votre projet et d'utiliser une analyse du codage social afin de comprendre les modèles d'interaction entre les développeurs. Vous pouvez analyser le code source GitHub avec les problèmes GitHub, les problèmes JIRA, ou les deux. Utilisez Developer Insights pour identifier les fichiers hautement susceptibles de générer des erreurs et examiner la conformité du projet avec les pratiques DevOps. L'analyse du codage social dans Team Dynamics identifie le niveau d'interaction entre les membres d'une équipe pour leur permettre de remédier à des pratiques non productives. 		|
|[Construisez votre propre chaîne d'outils ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain){:new_window}		|Cette chaîne d'outils ne comporte aucun outil préconfiguré. Si vous connaissez déjà les chaînes d'outils, vous pouvez configurer votre propre chaîne d'outils. 		|
{: caption="Tableau 2. Modèles de chaînes d'outils" caption-side="top"}
