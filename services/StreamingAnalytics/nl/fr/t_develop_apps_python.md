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

# Développement d'applications Python pour {{site.data.keyword.streaminganalyticsshort}}
{: #t_develop_apps_python}

Vous pouvez désormais développer des applications Python dans IBM Data Science Experience (DSX) ou dans votre environnement de développement Python local et déployer ces applications dans {{site.data.keyword.streaminganalyticsshort}}.
{:shortdesc}

Développez et déployez vos applications Python dans le cloud {{site.data.keyword.Bluemix_short}} en utilisant le service {{site.data.keyword.streaminganalyticsshort}} via l'une des méthodes ci-après :


## Développement d'applications Streams Python dans DSX
{: #t_develop_python_dsx}

Si vous ne disposez pas d'un environnement de développement Python, la façon la plus rapide de démarrer est d'utiliser nos fichiers notebook DSX et de créer des applications Python exemple pour le service {{site.data.keyword.streaminganalyticsshort}}. Ces fichiers notebook fournissent les procédures et les codes exemple pour créer et déployer des applications Python exemple simples pour le service {{site.data.keyword.streaminganalyticsshort}} au sein de l'environnement DSX Python :

* [Hello World!](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca9c6e8) : créez une application Hello World! simple pour démarrer puis déployez l'application dans une instance du service {{site.data.keyword.streaminganalyticsshort}}.

* [Healthcare Demo](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039cad29a6) : créez une application qui ingère et analyse les données en continu en provenance d'un flux puis les visualise dans le fichier notebook. Vous soumettez ensuite cette application à l'instance de service {{site.data.keyword.streaminganalyticsshort}}.

* [Neural Net Demo](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca60bb7) : créez un jeu de données exemple, créez un modèle pour les données exemple, utilisez ce modèle dans une application de diffusion en flux continu, visualisez le flux de données en continu et soumettez l'application de diffusion en flux continu dans le service {{site.data.keyword.streaminganalyticsshort}}.

## Développement d'applications dans votre environnement Python local
 {: #t_develop_python_api}

 L'[{{site.data.keyword.streamsshort}}API d'application Python](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), qui est incluse dans le package streamsx, vous permet de créer des applications de traitement de flux en utilisant les fonctions ou les classes appelables Python. Vous pouvez utiliser l'API d'application Python pour définir et soumettre ensuite l'application au service.

Démarrez en suivant les procédures du tutoriel [Developing for the {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) pour créer une application exemple dans votre environnement Python local puis le déployer dans le service {{site.data.keyword.streaminganalyticsshort}}.
