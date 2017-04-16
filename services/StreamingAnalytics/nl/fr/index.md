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


# Initiation à {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} tire sa puissance d'{{site.data.keyword.streamsshort}}, une plateforme d'analyse avancée que vous pouvez utiliser pour recevoir, analyser et mettre en corrélation les informations au fur et à mesure qu'elles arrivent depuis différentes sources de données en temps réel. Quand vous créez une instance du service {{site.data.keyword.streaminganalyticsshort}}, vous obtenez votre propre instance d'{{site.data.keyword.streamsshort}} s'exécutant dans le cloud {{site.data.keyword.Bluemix_short}}, prête à exécuter vos applications {{site.data.keyword.streamsshort}}.
{:shortdesc}

Vous pouvez déployer vos applications dans une instance {{site.data.keyword.streaminganalyticsshort}} qui s'exécute dans le cloud {{site.data.keyword.Bluemix_short}}.

Il vous est même possible d'utiliser directement {{site.data.keyword.streaminganalyticsshort}} en exécutant les [applications de démarrage](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}. Si vous souhaitez aller plus loin avec vos propres applications, vous aurez besoin d'un environnement de développement {{site.data.keyword.streamsshort}} et vous devrez faire en sorte que votre SPL soit prêt pour le cloud.

Pour démarrer avec {{site.data.keyword.streaminganalyticsshort}}, utilisez l'une des méthodes ci-après pour soumettre le bundle d'applications (fichier .sab) associé à votre application SPL ou Java™ :
* Utilisez la console {{site.data.keyword.streaminganalyticsshort}}.
* Développez une application {{site.data.keyword.Bluemix_short}} et ajoutez-y l'application {{site.data.keyword.streamsshort}}. Contrôlez-la en utilisant l'[API REST {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220). Vérifiez que vos applications SPL ou Java s'exécutent correctement dans votre environnement de développement.

Vous pouvez désormais utiliser {{site.data.keyword.streaminganalyticsshort}}
avec d'autres services {{site.data.keyword.Bluemix_short}}, dont {{site.data.keyword.cloudant}} et {{site.data.keyword.messagehub}}. Voir les [tutoriels traitant de l'intégration à d'autres services {{site.data.keyword.Bluemix_short}}](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window} pour des exemples permettant d'être directement opérationnel.

Pour développer une application {{site.data.keyword.streamsshort}}, vous devez disposer d'un environnement de développement {{site.data.keyword.streamsshort}}. Si vous n'avez pas d'environnement {{site.data.keyword.streamsshort}}, vous pouvez télécharger gratuitement {{site.data.keyword.streamsshort}} Quick Start Edition depuis la [page de produit {{site.data.keyword.streamsshort}}.](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)

Si vous ne maîtrisez pas le développement d'applications {{site.data.keyword.streamsshort}}, des ressources vous permettent de vous familiariser. Pour plus d'informations, voir [{{site.data.keyword.streamsshort}} Knowledge Center.](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

Si vous disposez déjà d'une application SPL exécutée sur site, vous devez [préparer votre application pour le cloud.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}
* [Introduction to {{site.data.keyword.streaminganalyticsshort}}](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} SDK for Node.js™ Starter Application](http://bit.ly/1iR1bzu){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} Liberty for Java™ Starter Application](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/){:new_window}
* [Getting your SPL application ready for the cloud](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud){:new_window}
* [Bluemix {{site.data.keyword.streaminganalyticsshort}} Development Guide](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-development-guide/){:new_window}
* [Autres tutoriels](StreamingAnalytics.html#r_integrating_cloudant_rest){:new_window}


## Référence d'API
{: #api}
* [{{site.data.keyword.streaminganalyticsshort}} API REST](https://console.ng.bluemix.net/apidocs/220){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} metrics using the {{site.data.keyword.streamsshort}} REST API](https://developer.ibm.com/bluemix/2016/07/25/streaming-analytics-metrics-using-rest-api/){:new_window}

## Contextes d'exécution compatibles
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## Liens connexes
{: #general}
* [{{site.data.keyword.streamsshort}} documentation](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [{{site.data.keyword.streamsshort}}Quick Start Edition](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}
