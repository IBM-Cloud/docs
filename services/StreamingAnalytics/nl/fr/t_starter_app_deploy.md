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

# Déploiement des applications de démarrage sur {{site.data.keyword.Bluemix_short}}
{: #starterapps_deploy}

Vous pouvez envoyer et déployer l'une des applications de démarrage {{site.data.keyword.streaminganalyticsshort}} vers le cloud {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

Avant de commencer, préparez {{site.data.keyword.Bluemix_short}} au déploiement des applications de démarrage {{site.data.keyword.streaminganalyticsshort}} :

* [Installez l'outil de ligne de commande cf](https://github.com/cloudfoundry/cli/releases).
* Créez une application dans {{site.data.keyword.Bluemix_short}}, ajoutez le service {{site.data.keyword.streaminganalyticsshort}} à votre application et reconstituez l'application :
	* Pour déployer l'application de démarrage de détection d'événements, créez une application avec une phase d'exécution {{site.data.keyword.sdk4node}}.
	* Pour déployer l'application de démarrage relative au trafic new-yorkais, créez une application avec une phase d'exécution Liberty for Java™.

Mémorisez le nom que vous attribuez à votre application ; vous en aurez besoin ultérieurement.

{{site.data.keyword.streaminganalyticsshort}} fournit deux applications exemple pour vous permettre de démarrer avec le service.

L'application de démarrage de détection d'événements analyse les données relatives à la météo dans un flux en temps réel et affiche le statut et les résultats de l'analyse. L'application est écrite en {{site.data.keyword.sdk4node}}. Pour plus de détails sur la façon d'utiliser l'application de démarrage de détection d'événements, voir [Detect complex events in a real-time data stream](https://www.ibm.com/developerworks/library/ba-bluemix-detect-complex-events-from-data-stream-trs/index.html).

L'application de démarrage relative au trafic new-yorkais lit et analyse les données de trafic depuis un site Web public. L'application est écrite en Liberty for Java. Pour plus de détails sur la façon d'utiliser l'application de démarrage relative au trafic new-yorkais, voir [{{site.data.keyword.streaminganalyticsfull}} Starter Application](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/).

Pour télécharger et déployer l'application de démarrage dans {{site.data.keyword.Bluemix_short}} :

1. Téléchargez les applications de démarrage relatives à la [détection d'événements](https://hub.jazz.net/project/streamscloud/EventDetection/overview) ou au [trafic new-yorkais](https://hub.jazz.net/project/streamscloud/NYCTraffic/overview).
2. Sur la ligne de commande, allez dans le répertoire de projet.
  <pre><code>cd mon_app</code></pre>
  {:pre}

3. Renommez le répertoire de projet pour qu'il porte le même nom que celui que vous avez donné à votre application dans {{site.data.keyword.Bluemix_short}}.
4. Connectez-vous à {{site.data.keyword.Bluemix_short}}:
  <pre><code>cf api https://api.DomainName</code></pre>
  {:pre}

5. Connectez-vous à {{site.data.keyword.Bluemix_short}} et définissez votre organisation cible quand vous y êtes invité :
  <pre><code>cf login</code></pre>
  {:pre}

6. Déployez votre application :
  <pre><code>cf push mon_app</code></pre>
  {:pre}

7. Accédez à la page de présentation de votre application, accessible depuis le tableau de bord {{site.data.keyword.Bluemix_short}}, afin de vérifier que votre application a bien démarré.
8. Lancez votre application pour l'afficher dans votre navigateur. Vous trouverez l'adresse URL (ou "route") de votre application dans la page de
présentation de l'application.

A présent que votre application est en cours d'exécution, vous pouvez accéder au tableau de bord du service pour voir le statut de votre instance {{site.data.keyword.streaminganalyticsshort}} et obtenir des informations pour le traitement des incidents. Pour accéder au tableau de bord du service, allez dans le tableau de bord {{site.data.keyword.Bluemix_short}} et cliquez sur la vignette {{site.data.keyword.streaminganalyticsshort}} dans la page de présentation de l'application.
