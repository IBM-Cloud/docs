---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

Le applicazioni Liberty for Java su {{site.data.keyword.Bluemix}} si avvalgono del pacchetto di build liberty-for-java. Il pacchetto di build liberty-for-java fornisce un ambiente di runtime completo per eseguire applicazioni Java EE 7 e OSGi sul profilo Liberty. Supporta framework di uso comune come Spring e include l'IBM JRE. WebSphere Liberty abilita un rapido sviluppo delle applicazioni che è adatto per il cloud.
{: shortdesc}

## Rilevamento
{: #detection}
Il pacchetto di build Liberty viene utilizzato quando i seguenti tipi di applicazioni sono distribuiti:
* [File WAR](optionsForPushing.html#stand_alone_apps)
* [File EAR](optionsForPushing.html#stand_alone_apps)
* [Directory server Liberty](optionsForPushing.html#server_directory)
* [Server in pacchetto Liberty](optionsForPushing.html#packaged_server)
* Java principale
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Applicazione starter
{: #starter_application}
{{site.data.keyword.Bluemix}} fornisce diverse applicazioni starter Liberty.  Le applicazioni starter Liberty sono applicazioni Liberty semplici che forniscono un template che puoi utilizzare. Puoi sperimentare le applicazioni starter ed effettuare e inviare modifiche all'ambiente Bluemix.  Consulta [Utilizzo di applicazioni starter](/docs/cfapps/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [Gestione delle applicazioni Liberty](/docs/manageapps/app_mng.html#Utilities)
* [Distribuzione di applicazioni con IBM Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [Introduzione al servizio IBM Monitoring and Analytics per Bluemix](/docs/services/monana/index.html#monana_oview)

