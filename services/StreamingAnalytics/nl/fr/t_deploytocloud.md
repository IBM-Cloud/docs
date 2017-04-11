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

#Déploiement d'applications {{site.data.keyword.streamsshort}} dans le cloud
{: #t_deploytocloud}

Vous pouvez déployer vos applications {{site.data.keyword.streamsshort}} dans une instance {{site.data.keyword.streaminganalyticsshort}} s'exécutant dans le cloud {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

Les applications {{site.data.keyword.streamsshort}} sont écrites en langage {{site.data.keyword.streamsshort}} Processing Language (SPL) dans un environnement {{site.data.keyword.streamsshort}}. {{site.data.keyword.streamsshort}} prend également en charge plusieurs kits de développement Java™ que vous pouvez utiliser pour développer vos applications. Pour plus d'informations sur la prise en charge Java dans {{site.data.keyword.streamsshort}}, voir [Kits de développement Java pris en charge pour le développement d'application](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}.
{{site.data.keyword.streaminganalyticsshort}} n'inclut pas de développement d'environnement {{site.data.keyword.streamsshort}} dans le cloud mais vous pouvez déployer les applications que vous développez localement dans le cloud.

Avant de commencer, désactivez le logiciel de blocage d'incrustation de votre navigateur pour afficher la console Streaming Analytics.

Pour déployer vos applications {{site.data.keyword.streamsshort}} dans le cloud :

1. Configurez un environnement {{site.data.keyword.streamsshort}} pour développer et tester votre application. 

	Si vous n'avez pas d'environnement {{site.data.keyword.streamsshort}}, vous pouvez télécharger {{site.data.keyword.streamsshort}} Quick Start Edition, gratuitement. Accédez à la [page de produit IBM Streams](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window} et cliquez sur **Download the native software installation**.

2. Développez votre application SPL ou Java application dans votre environnement {{site.data.keyword.streamsshort}} en utilisant Streams Studio ou les outils de ligne de commande.
3. Vérifiez que vos applications SPL ou Java s'exécutent correctement dans votre environnement de développement.
4. Soumettez le bundle d'applications (fichier .sab) associé à votre application SPL ou Java dans votre instance de service du cloud en utilisant l'une des méthodes suivantes :
	* Utilisez la console {{site.data.keyword.streaminganalyticsshort}} pour soumettre le bundle d'applications.
    * Développez une application {{site.data.keyword.Bluemix_short}} et ajoutez-y l'application {{site.data.keyword.streamsshort}}. Contrôlez-la en utilisant l'API REST {{site.data.keyword.streaminganalyticsshort}}.

Votre application est maintenant déployée dans le cloud. Vous pouvez la surveiller à l'aide du service {{site.data.keyword.streaminganalyticsshort}}. Vous pouvez également soumettre plusieurs applications SPL ou Java (fichiers .sab) dans votre instance de service, sans limite de nombre.
