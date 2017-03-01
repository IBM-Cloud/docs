---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# A propos de 
{: #about}

Vous pouvez effectuer une analyse en temps réel sur des données en mouvement dans le cadre de vos applications {{site.data.keyword.Bluemix_short}} en utilisant {{site.data.keyword.streaminganalyticsfull}}. 
{:shortdesc}

{{site.data.keyword.streaminganalyticsshort}} tire sa puissance d'{{site.data.keyword.streamsshort}}, une plateforme d'analyse avancée que vous pouvez utiliser pour recevoir, analyser et mettre en corrélation les informations au fur et à mesure qu'elles arrivent depuis différentes sources de données en temps réel. Quand vous créez une instance du service {{site.data.keyword.streaminganalyticsshort}}, vous obtenez votre propre instance d'{{site.data.keyword.streamsshort}} s'exécutant dans le cloud {{site.data.keyword.Bluemix_short}}, prête à exécuter vos applications {{site.data.keyword.streamsshort}}.

Vous utilisez {{site.data.keyword.streaminganalyticsshort}} pour la première fois ? Découvrez une [rapide introduction au service](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix-2/){:new_window}. Si vous souhaitez aller plus loin avec vos propres applications, vous aurez besoin d'un environnement de développement {{site.data.keyword.streamsshort}} et vous devrez faire en sorte que votre SPL soit prêt pour le cloud.

Le service {{site.data.keyword.streaminganalyticsshort}} fournit les fonctionnalités ci-après permettant de déployer, d'analyser et de surveiller vos données sur le cloud :

**Utilisation interactive et par programme du service :**

Vous pouvez utiliser interactivement le service via la [console {{site.data.keyword.streaminganalyticsshort}}](/docs/services/StreamingAnalytics/c_streams_console.html), ou bien par programme via l'[API REST {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220){:new_window}.

**Déploiement et surveillance d'applications SPL et Java :**

{{site.data.keyword.streamsfull}} Processing Language (SPL) est un langage de programmation utilisé pour créer des applications de traitement de flux. Vous pouvez écrire des applications {{site.data.keyword.streamsshort}} en langage SPL ou Java. [Déployez et surveillez ces applications](/docs/services/StreamingAnalytics/t_deploytocloud.html) en utilisant {{site.data.keyword.streaminganalyticsshort}}. 

**Compatibilité avec les opérateurs {{site.data.keyword.streamsshort}} :**

Les opérateurs {{site.data.keyword.streamsshort}} du kit d'outils standard [{{site.data.keyword.streamsshort}} Processing Language (SPL) doivent tous être compatibles](/docs/services/StreamingAnalytics/c_beta_adapters.html) avec {{site.data.keyword.streaminganalyticsshort}}.

## Responsabilités {{site.data.keyword.streaminganalyticsfull}} 

### Responsabilités du client

Le client est responsable des actions suivantes :

* Suivi de la configuration IBM initiale d'{{site.data.keyword.streamsshort}}, surveillance, configuration et gestion des travaux {{site.data.keyword.streamsshort}} s'exécutant dans son instance. Le client peut démarrer et arrêter l'instance, et il peut démarrer et arrêter jobskeywordnning sur l'instance.
* Développement, si nécessaire ou obligatoire, de programmes et d'applications sur le service pour analyser les données et en tirer des renseignements utiles. Le client est aussi responsable de la qualité et des performances des programmes et applications ainsi développés. Les programmes peuvent être développés en SPL, Java ou d'autres langages pris en charge, via la fonction {{site.data.keyword.streamsshort}} Topology. Ils doivent être compilés en se servant d'{{site.data.keyword.streamsshort}} Developer Edition ou de {{site.data.keyword.streamsshort}} Quick Start Edition, avec le même système d'exploitation que celui utilisé pour {{site.data.keyword.streaminganalyticsshort}}. 
* Vérification périodique du lien suivant, pour être informé d'une période d'indisponibilité planifiée, avec ou sans interruption - [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}  
* Sauvegarde de toutes les données, métadonnées, fichiers de configuration et paramètres d'environnement, en fonction des exigences de l'environnement, afin d'assurer une continuité.
* Restauration des données, métadonnées, fichiers de configuration et paramètres d'environnement depuis une sauvegarde, afin d'assurer une continuité, dans l'éventualité d'un incident, quel qu'en soit son type, survenant dans un centre de données, un pod, un serveur, un disque dur ou un logiciel, par exemple.

### Responsabilités d'IBM

Dans le cadre d'{{site.data.keyword.streaminganalyticsfull}}, IBM est responsable des actions suivantes :

* Fournir et gérer une infrastructure de serveurs, de stockage et de mise en réseau pour l'instance client. 
* Fournir une configuration initiale d'{{site.data.keyword.streamsshort}} sur le nombre de noeuds sélectionnés.
* Fournir et gérer une infrastructure pour Internet et un pare-feu interne pour la protection et l'isolation. 
* Surveiller et gérer les composants ci-après sur {{site.data.keyword.streaminganalyticsfull}} :
	* Composants réseau
	* Serveurs et espace de stockage local associé
	* Systèmes d'exploitation des infrastructures
	* Services de gestion {{site.data.keyword.streamsshort}}
	* Instances {{site.data.keyword.streamsshort}} 
* Fournir des correctifs de maintenance, incluant les correctifs de sécurité appropriés pour les systèmes d'exploitation des infrastructures et {{site.data.keyword.streamsshort}}.
* Effectuer d'une part, une maintenance régulière ne devant provoquer aucune période d'indisponibilité du système (maintenance “sans interruption”) et d'autre part, une maintenance pouvant générer une période d'indisponibilité du système ainsi qu'un redémarrage (maintenance “avec interruption”), à des dates précises, planifiées et publiées sur [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window} 
* Tout changement dans les dates et heures de la maintenance planifiée sera publié, avec un avis préalable approprié. 
