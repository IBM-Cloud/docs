---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introduzione a Insights for Weather
{: #insights_weather_overview}

*Ultimo aggiornamento: 19 maggio 2016*

Utilizza {{site.data.keyword.weatherfull}} per incorporare i dati meteo da
The Weather Company (TWC) nelle tue applicazioni {{site.data.keyword.Bluemix}}.
{:shortdesc}

**Nota:** il servizio Insights for Weather non è attualmente disponibile in Giappone.

Prima di iniziare, crea un'applicazione web {{site.data.keyword.Bluemix_notm}} nel dashboard con un runtime come Liberty for Java. Attendi il provisioning della tua applicazione e aggiungi quindi il servizio Insights for Weather alla tua applicazione.

Quando esegui il bind della tua applicazione a Insights for Weather, stai eseguendo il provisioning di un'istanza del servizio
con credenziali univoche. La tua applicazione utilizza queste credenziali con le [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window} per richiamare i dati meteo.

Attieniti alla seguente procedura per richiamare le credenziali `VCAP_SERVICES` e integrare l'istanza del servizio con la tua applicazione.

1. Passa alla pagina della panoramica della tua applicazione.
2. Vai alla sezione **Variabili di ambiente**. Vengono visualizzate le informazioni su `VCAP_SERVICES` per ognuno dei tuoi servizi.
3. Prendi nota dei valori nome utente e password dal servizio Insights for Weather.
Per provare le [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window},
devi immettere queste credenziali quando ti vengono richieste all'accesso.
Il tuo `VCAP_SERVICES` sarà simile al seguente esempio:

```
{
   "weatherinsights": [
     {
      "name": "Insights for Weather",
      "label": "weatherinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "twcservice.mybluemix.net",
         "password": "7abcxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }
   ]
}
```

**Nota:** ogni regione è indipendente. Non puoi utilizzare le credenziali di servizio
che ti sono state fornite in una regione per autenticarti a un servizio in un'altra regione.
La mancata immissione delle credenziali corrette comporterà il ricevimento di un messaggio "Non autorizzato" nel corpo della risposta. 

# rellinks
{: #rellinks}
## samples
{: #samples}
* [Demo di Insights for Weather](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## api
{: #api}
* [API REST](https://twcservice.{APPDomain}/rest-api/){: new_window}

## runtime compatibili
{: #buildpacks}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## general
{: #general}
* [Aggiunta di un servizio alla tua applicazione](../reqnsi.html){: new_window}
* [Sviluppo end-to-end](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Listino prezzi di {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Prerequisiti di {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
