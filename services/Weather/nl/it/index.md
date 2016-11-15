---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introduzione a {{site.data.keyword.weather_short}}
{: #insights_weather_overview}

Utilizza {{site.data.keyword.weatherfull}} per incorporare i dati meteo da
The Weather Company (TWC) nelle tue applicazioni {{site.data.keyword.Bluemix}}.
{:shortdesc}

**Attenzione:** attualmente, il servizio {{site.data.keyword.weather_short}} **non può** essere acquistato o
utilizzato nei seguenti paesi o regioni: Afghanistan, Armenia, Azerbaijan,
Bahrain, Bangladesh, Bhutan, Brunei, Cambogia, Cina, Cipro, Georgia,
Indonesia, Iran, Iraq, Giappone, Giordania, Kazakhstan, Kuwait, Kyrgyzstan, Laos,
Libano, Malesia, Maldive, Mongolia, Myanmar, Nepal, Oman, Pakistan, Filippine,
Qatar, Russia, Arabia Saudita, Singapore, Corea del sud, Sri Lanka, Siria,
Tajikistan, Timor-Leste, Turchia, Turkmenistan, Emirati arabi uniti,
Uzbekistan, Vietnam, Yemen.. Questo elenco viene aggiornato quando sono disponibili ulteriori informazioni.

Se disponi di un'applicazione esistente che utilizza il
[servizio Insights for Weather](https://console.{DomainName}/docs/services/InsightsWeather/index.html){: new_window},
la tua applicazione continuerà a funzionare senza alcuna modifica per 90 giorni dopo l'introduzione di
{{site.data.keyword.weather_short}}. Per usufruire dei benefici delle nuove API aggiunte
e migliorare il modello dei prezzi, puoi migrare la tua applicazione al nuovo servizio. 

Prima di iniziare, crea un'applicazione web {{site.data.keyword.Bluemix_notm}} nel dashboard
con un runtime come Liberty for Java. Attendi il provisioning della tua applicazione e quindi
aggiungi il servizio {{site.data.keyword.weather_short}} alla tua applicazione.

Quando hai eseguito il bind della tua applicazione a {{site.data.keyword.weather_short}}, stai eseguendo il provisioning di un'istanza di servizio
con credenziali univoche. La tua applicazione utilizza queste credenziali con le
[API REST](https://twcservice.{APPDomain}/rest-api/){:new_window} per richiamare i dati meteo.

Segui questi passi per richiamare le credenziali del servizio da `VCAP_SERVICES`
e integra l'istanza del servizio con la tua applicazione.

1. Passa alla pagina della panoramica della tua applicazione.
2. Vai alla sezione **Variabili di ambiente**. Vengono visualizzate le informazioni su `VCAP_SERVICES` per ognuno dei tuoi servizi.
3. Prendi nota dei valori nome utente e password dal servizio {{site.data.keyword.weather_short}}.
Per provare le [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window},
devi immettere le credenziali quando ti vengono richieste all'accesso.
Il tuo `VCAP_SERVICES` sarà simile al seguente esempio:

```
{
{
   "weatherinsights": [
      {
         "name": "Weather Company Data for IBM Bluemix",
         "label": "weatherinsights",
         "plan": "Free",
         "credentials": {
            "username": "d40845df-8125-441f-8e7c-e650726ce721",
            "password": "tDV0HGZz3O",
            "host": "twcservice.mybluemix.net",
            "port": 443,
            "url": "https://d40845df-8125-441f-8e7c-e650726ce721:tDV0HGZz3O@twcservice.mybluemix.net"
         }
      }
   ]
}
```

**Nota:** ogni regione è indipendente. Non puoi utilizzare le credenziali di servizio
che ti sono state fornite in una regione per autenticarti a un servizio in un'altra regione.
La mancata immissione delle credenziali corrette comporterà il ricevimento di un messaggio *Non autorizzato* nel corpo della risposta.

# rellinks
{: #rellinks}
## samples
{: #samples}
* [{{site.data.keyword.weather_short}} demo app](http://weather-company-data-demo.{APPDomain}){: new_window}
* [{{site.data.keyword.weather_short}} Deep Dive video](https://youtu.be/pZHXIibziUo){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [{{site.data.keyword.Bluemix_notm}} + Weather sample app](https://github.com/IBM-Bluemix/insights-weather){: new_window}
* [IBM Cloud - Bare Metal, NYC Taxi Data, and Insights for Weather (YouTube tutorial)](https://www.youtube.com/watch?v=Uwmzpx9DZ5c){: new_window}

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
* [Aggiunta di un servizio alla tua applicazione](/docs/services/reqnsi.html){: new_window}
* [Sviluppo end-to-end](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Listino prezzi di {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Prerequisiti di {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
