---

copyright:
  years: 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introduzione a Insights for Twitter {: #insights_twitter_overview}

Utilizza {{site.data.keyword.twitterfull}} per incorporare il contenuto di Twitter dai flussi Twitter [Decahose](http://support.gnip.com/gnip2.0/){: new_window} o [PowerTrack](http://support.gnip.com/apis/powertrack2.0/){: new_window} nelle tue applicazioni {{site.data.keyword.Bluemix}}.
{:shortdesc}

Per iniziare a utilizzare {{site.data.keyword.twittershort}}, crea prima la tua applicazione web Bluemix con un runtime come Liberty for Java e aggiungi quindi il
servizio {{site.data.keyword.twittershort}} alla tua applicazione. Quando il servizio {{site.data.keyword.twittershort}} è associato alla tua applicazione,
il provisioning dell'istanza del servizio viene eseguito con delle credenziali univoche. La tua applicazione utilizza queste credenziali con le API REST per cercare e utilizzare il contenuto di Twitter.  Completa i seguenti passi per richiamare le credenziali da VCAP_SERVICES e integrare l'istanza del servizio con la tua applicazione.

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

## compatible runtimes
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

