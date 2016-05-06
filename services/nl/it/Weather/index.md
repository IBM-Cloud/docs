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

*Ultimo aggiornamento: 06 aprile 2016*

Utilizza {{site.data.keyword.weatherfull}} per incorporare i dati meteo da
The Weather Company (TWC) nelle tue applicazioni {{site.data.keyword.Bluemix}}.
{:shortdesc}

Le seguenti istruzioni ti guidano durante il processo di creazione di un'applicazione,
di bind dell'applicazione al servizio Insights for Weather e nel richiamo delle credenziali di servizio
per interagire con le [API REST](https://twcservice.{APPDomain}/rest-api/).

### Crea un'applicazione
{: #create_an_app}

Per scopi dimostrativi, crea un'applicazione utilizzando il runtime Liberty for Java,
ma il seguente processo generale può essere applicato ad altri runtime.

1. Se non disponi di un'applicazione esistente, nel dashboard, fai clic su **CREA APPLICAZIONE**.
2. Quando ti sarà richiesto di scegliere il template dell'applicazione, fai clic su **WEB**.
3. Quando ti sarà richiesto di scegliere uno starter, fai clic su **Liberty for Java**.
4. Fai clic su **Continua**.
5. Nel campo **Nome applicazione**, immetti il nome della tua applicazione.
6. Fai clic su **Fine**. Attendi il provisioning della tua applicazione.

### Aggiungi il servizio Insights for Weather
{: #add_insights_for_weather_service}

Segui questi passi per aggiungere il servizio Insights for Weather alla tua applicazione.
1. Apri il menu **Catalogo**.
2. Dalla sezione **Data & Analytics**, fai clic sul tile **Insights for Weather**.
3. Nell'elenco a discesa **Applicazione**, seleziona la tua applicazione.
4. Fai clic su **UTILIZZA**.
5. Quando richiesto, fai clic su **Riprepara** per riavviare la tua applicazione.

### Recupera le credenziali di Weather
{: #retrieve_weather_credentials}

Quando hai eseguito il bind della tua applicazione a Insights for Weather, stai eseguendo il provisioning di un'istanza di servizio
con credenziali univoche. Queste credenziali vengono memorizzate nel
`VCAP_SERVICES` della tua applicazione e sono essenziali per supportare l'interazione tra i servizi.

1. Passa alla pagina della panoramica della tua applicazione.
2. Vai alla sezione **Variabili di ambiente**. Vengono visualizzate le informazioni su `VCAP_SERVICES` per ognuno dei tuoi servizi.
3. Prendi nota dei valori nome utente e password dal servizio Insights for Weather.
Per provare le [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window},
devi immettere le credenziali quando ti vengono richieste all'accesso.
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

# rellinks
## samples
* [Demo di Insights for Weather](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## api
* [API REST](https://twcservice.{APPDomain}/rest-api/){: new_window}

## runtime compatibili {:id="buildpacks"}
* [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## general
* [Informazioni su Insights for Weather](https://console.{DomainName}/docs/services/Weather/weather_overview.html){: new_window}
* [Aggiunta di un servizio alla tua applicazione](https://console.{DomainName}/docs/services/reqnsi.html#add_service){: new_window}
* [Sviluppo end-to-end](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Listino prezzi di {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Prerequisiti di {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
