{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introduzione a Insights for Twitter {: #insights_twitter_overview}

*Ultimo aggiornamento: 13 maggio 2016*
{: .last-updated}

Utilizza {{site.data.keyword.twitterfull}} per incorporare il contenuto di Twitter dai flussi Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} o [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} nelle tue applicazioni {{site.data.keyword.Bluemix}}.
{:shortdesc}

Per iniziare ad utilizzare {{site.data.keyword.twittershort}}, crea la tua applicazione web Bluemix con un runtime come Liberty for Java, quindi aggiungi il servizio {{site.data.keyword.twittershort}} alla tua applicazione. Quando il servizio {{site.data.keyword.twittershort}} è associato alla tua applicazione, viene eseguito il provisioning dell'istanza del servizio con credenziali univoche. La tua applicazione utilizza queste credenziali con le API REST per cercare e utilizzare il contenuto di Twitter.  Completa i seguenti passi per richiamare le credenziali da VCAP_SERVICES e integrare l'istanza del servizio con la tua applicazione.

1. Passa alla pagina della panoramica sull'applicazione.
2. Vai alla sezione **Variabili d'ambiente**. Vengono visualizzate le informazioni `VCAP_SERVICES` per ognuno dei tuoi servizi.
3. Prendi nota dei valori per il nome utente e la password dal servizio {{site.data.keyword.twittershort}}. Per verificare le operazioni nella documentazione di riferimento API REST, avrai bisogno di immettere queste credenziali. Ad esempio, la tua `VCAP_SERVICES` sarà simile al seguente frammento:

```
{  
   "twitterinsights": [    
     {      
      "name": "IBM Insights for Twitter-x3",
      "label": "twitterinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "cdeservice.mybluemix.net",
         "password": "7cunxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }  
   ]
}
```

<!--
## Adding Insights for Twitter to your application {: #adding_twitter}

The following instructions guide you through the process of creating an application, binding the application to the {{site.data.keyword.twittershort}} service, and retrieving the service credentials to interact with REST API operations in the provided API reference documentation.

### Create an application
For demonstration purposes, you'll create an application using the Liberty for Java&trade;  runtime, but the general process described below can be applied to other runtimes. If you don't have an existing application, click **CREATE AN APP** in the dashboard. When asked to confirm the type of app, click **WEB**.

1. Open the **Catalog** menu.
2. From the **Runtimes** section, click **Liberty for Java**.
3. Click **Create**.
4. In the **App Name** field, specify the name of your app.
5. Click **Finish**. Wait for your application to provision.

### Add the Insights for Twitter service
Follow these steps to add the {{site.data.keyword.twittershort}} service to your app.

1. Open the **Catalog** menu.
2. From the **Data & Analytics** section, click the {{site.data.keyword.twittershort}} tile.
3. In the **App** field, select the name of your app.
4. Click **Create**.
5. When prompted, click **Restage** to restart your application.
-->

# rellinks
{: #rellinks}
## samples
{: #samples}
* [Interactive decahose search demo](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks: Tutorial and source code for decahose search demo](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [Analyzing "American Sniper" box office data (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## api
{: #api}
* [API REST ](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## runtime compatibili
{: #buildpacks}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## general
{: #general}
* [Novità nei servizi {{site.data.keyword.Bluemix_notm}}](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [Aggiunta di un servizio alla tua applicazione](../reqnsi.html){: new_window}
* [Sviluppo end-to-end](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Listino prezzi di {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Prerequisiti di {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

