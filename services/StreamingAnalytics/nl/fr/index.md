---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

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

Utilisez directement {{site.data.keyword.streaminganalyticsshort}} en exécutant les [applications de démarrage](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}.

Pour commencer à vous servir de {{site.data.keyword.streaminganalyticsshort}}, utilisez l'une des méthodes ci-après pour soumettre le bundle d'applications (fichier .sab) associé à votre application SPL, Java™, Python ou Scala Streams :
* Utilisez le bouton **Soumettre un travail** dans la console {{site.data.keyword.streaminganalyticsshort}}.
* Développez une application {{site.data.keyword.Bluemix_short}} et ajoutez-y l'application {{site.data.keyword.streamsshort}}. Contrôlez-la en utilisant l'[API REST {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220).


Utilisez {{site.data.keyword.streaminganalyticsshort}} avec d'autres services {{site.data.keyword.Bluemix_short}}, dont {{site.data.keyword.cloudant}} et {{site.data.keyword.messagehub}}. Voir les [tutoriels traitant de l'intégration à d'autres services {{site.data.keyword.Bluemix_short}}](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window} pour des exemples permettant d'être directement opérationnel.

Si vous voulez aller plus loin avec vos propres applications, vous pouvez obtenir un environnement de développement {{site.data.keyword.streamsshort}} et vous devez faire en sorte que votre application soit prête pour le cloud. Si vous n'avez pas d'environnement {{site.data.keyword.streamsshort}}, vous pouvez télécharger gratuitement {{site.data.keyword.streamsshort}} Quick Start Edition depuis la [page de produit {{site.data.keyword.streamsshort}}.](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)

Si vous ne maîtrisez pas le développement d'applications {{site.data.keyword.streamsshort}}, des ressources vous permettent de vous familiariser. Pour plus d'informations, voir [{{site.data.keyword.streamsshort}} Knowledge Center.](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

Si vous disposez déjà d'une application SPL exécutée sur site, vous devez [préparer votre application pour le cloud.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

**Remarque :** vous devez compiler vos applications sous Red Hat Enterprise Linux (RHEL) 6.5 ou une version CentOS équivalente, utilisant des processeurs Intel.

## Applications Python {{site.data.keyword.streamsshort}} pour {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted_py notoc}

Vous pouvez désormais créer des applications Streams dans un environnement Python, comme IBM Data Science Experience (DSX), et soumettre ces applications dans l'instance {{site.data.keyword.streaminganalyticsshort}} pour qu'elle soit déployée dans le cloud Bluemix. Vous n'avez plus besoin d'installer {{site.data.keyword.streamsshort}} localement pour compiler et déployer une application Streams Python.

Démarrez en créant des applications Streams Python exemple utilisant Jupyter Notebook dans DSX, et soumettez ces applications à l'instance de service directement depuis DSX. Pour plus d'informations, voir [Développement d'applications Streams Python dans DSX](/docs/services/StreamingAnalytics/t_develop_apps_python.html#t_develop_python_dsx).

{{site.data.keyword.streaminganalyticsshort}} prend également en charge le déploiement d'applications Streams depuis votre environnement Python local. Vous devez utiliser l'[API d'application Python {{site.data.keyword.streamsshort}}](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), qui est incluse dans le package streamsx pour développer vos applications Python localement et les soumettre à l'instance de service. Pour démarrer, suivez les procédures du tutoriel [Developing for the IBM {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html).
